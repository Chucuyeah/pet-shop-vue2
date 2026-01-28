<template>
  <header
    class="main-header"
    :class="{ 'header-merged': isMerged }"
    ref="header"
  >
    <div class="header-content">
      <div class="brand-text">
        <span 
          class="word" 
          :class="{ active: activeWord === 0 }"
          @click="scrollToSection('grooming')"
        >Grooming</span>
        <span 
          class="word highlight" 
          :class="{ active: activeWord === 1 }"
          @click="scrollToSection('food')"
        >Food</span>
        <span 
          class="word" 
          :class="{ active: activeWord === 2 }"
          @click="scrollToSection('clinic')"
        >Clinic</span>
      </div>
    </div>
  </header>
</template>

<script>
import gsap from "gsap"
import ScrollTrigger from "gsap/ScrollTrigger"
import ScrollToPlugin from "gsap/ScrollToPlugin"

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin)

export default {
  name: "Header",

  data() {
    return {
      isMerged: false,
      activeWord: 0
    }
  },

  mounted() {
    this.initScrollAnimation()
  },

  methods: {
    initScrollAnimation() {
      ScrollTrigger.create({
        trigger: document.body,
        start: "top top",
        end: "+=300",
        onUpdate: (self) => {
          this.isMerged = self.progress > 0.3
        }
      })
    },

    setActiveWord(index) {
      this.activeWord = index
    },

    scrollToSection(id) {
      if (window.lenis) {
        window.lenis.scrollTo(`#${id}`, {
          duration: 1.2,
          easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)) 
        })
      } else {
        gsap.to(window, {
          duration: 1,
          scrollTo: {
            y: `#${id}`,
            autoKill: true
          },
          ease: "power3.inOut"
        })
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.main-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 40px 60px;
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  pointer-events: auto;

  &.header-merged {
    padding: 30px 60px;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(20px);
    box-shadow: 0 2px 20px rgba(74, 144, 226, 0.08);
  }
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
}

.brand-text {
  display: flex;
  gap: 12px;
  font-size: 28px;
  font-weight: 500;
  letter-spacing: -0.5px;

  .word {
    color: rgba(74, 144, 226, 0.4);
    transition: all 0.4s ease;
    cursor: pointer;
    position: relative;
    z-index: 10; 

    &:hover {
      color: #4A90E2;
      transform: translateY(-2px);
    }

    &.highlight {
      color: #4A90E2;
    }

    &.active {
      color: #4A90E2;
      text-shadow: 0 0 20px rgba(74, 144, 226, 0.3);
    }
  }
}



/* Tablet */
@media (max-width: 1024px) and (min-width: 769px) {
  .main-header {
    padding: 35px 50px;

    &.header-merged {
      padding: 25px 50px;
    }
  }

  .brand-text {
    font-size: 26px;
    gap: 10px;
  }
}

/* Mobile  */
@media (max-width: 768px) {
  .main-header {
    padding: 20px 24px;

    &.header-merged {
      padding: 15px 24px;
      box-shadow: 0 2px 15px rgba(74, 144, 226, 0.1);
    }
  }

  .brand-text {
    font-size: 20px;
    gap: 8px;
  }
}

@media (max-width: 480px) {
  .main-header {
    padding: 16px 20px;

    &.header-merged {
      padding: 12px 20px;
    }
  }

  .brand-text {
    font-size: 18px;
    gap: 6px;
    
    .word {
      &.active {
        text-shadow: 0 0 15px rgba(74, 144, 226, 0.25);
      }
    }
  }
}
</style>
