<template>
  <Index />
</template>

<script>
import Index from "./pages/Index.vue"
import Lenis from 'lenis'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

export default {
  components: {
    Index
  },
  mounted() {
    this.initLenis()
  },
  methods: {
    initLenis() {
      const lenis = new Lenis()
      
      // Store on window for global access (e.g., from Header)
      window.lenis = lenis

      lenis.on('scroll', ScrollTrigger.update)

      gsap.ticker.add((time) => {
        lenis.raf(time * 1000)
      })

      gsap.ticker.lagSmoothing(0)
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  overflow-x: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  
  /* Responsive base font size */
  @media (max-width: 768px) {
    font-size: 14px;
  }
  
  @media (max-width: 480px) {
    font-size: 13px;
  }
}

/* Prevent horizontal scroll on mobile */
html {
  overflow-x: hidden;
}
</style>
