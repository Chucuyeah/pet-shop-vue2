<template>
  <section class="step-section" ref="section">
    <div class="pin-container">

      <!-- TEXT OVERLAY -->
      <div 
        v-for="(step, index) in steps" 
        :key="`text-${index}`"
        class="step-text-wrapper"
        :style="getTextStyle(index)"
      >
        <h1 class="step-text">{{ step.title }}</h1>
      </div>

      <!-- IMAGE LAYER -->
      <div 
        v-for="(step, index) in steps" 
        :key="`image-${index}`"
        class="step-image-wrapper"
        :style="getImageStyle(index)"
      >
        <div class="image-container">
          <img :src="step.image" :alt="step.title" />
        </div>
      </div>

    </div>
  </section>
</template>

<script>
import gsap from "gsap"
import ScrollTrigger from "gsap/ScrollTrigger"

gsap.registerPlugin(ScrollTrigger)

export default {
  name: "SectionTwo",

  data() {
    return {
      steps: [
        { 
          title: "Pet Grooming", 
          image: require("@/assets/images/grooming.jpeg") 
        },
        { 
          title: "Healthy Food", 
          image: require("@/assets/images/food.jpeg") 
        },
        { 
          title: "Veterinary Clinic", 
          image: require("@/assets/images/clinic.jpeg") 
        }
      ],
      scrollProgress: 0
    }
  },

  mounted() {
    ScrollTrigger.create({
      trigger: this.$refs.section,
      start: "top top",
      end: "+=250%", // Jarak scroll virtual yang konsisten
      pin: true,
      pinSpacing: true, // Berikan ruang setelah pin selesai untuk section 3
      scrub: 0.5,
      anticipatePin: 1,
      onUpdate: (self) => {
        this.scrollProgress = self.progress
      }
    })
  },

  methods: {
    getTextStyle(index) {
      const stepsCount = this.steps.length
      const stepProgress = this.scrollProgress * stepsCount
      
      const stepStart = index
      const textEnd = index + 0.6 // Diperlama dari 0.4 ke 0.6
      
      let opacity = 0
      let scale = 0.8
      
      if (stepProgress >= stepStart && stepProgress < textEnd) {
        // Fade in text lebih lambat/halus
        const progress = (stepProgress - stepStart) / 0.6
        opacity = Math.min(progress, 1)
        scale = 0.8 + (Math.min(progress, 1) * 0.2)
      } else if (stepProgress >= textEnd && stepProgress < index + 0.9) {
        // Fade out text
        const fadeOut = (stepProgress - textEnd) / 0.3
        opacity = 1 - fadeOut
        scale = 1
      }
      
      return {
        opacity: Math.max(opacity, 0),
        transform: `scale(${scale})`,
        zIndex: 10 + index
      }
    },

    getImageStyle(index) {
      const stepsCount = this.steps.length
      const stepProgress = this.scrollProgress * stepsCount
      
      const imageStart = index + 0.2 // Gambar mulai muncul lebih awal (dari 0.3 ke 0.2)
      const imageEnd = index + 1
      
      let opacity = 0
      let scale = 1.3
      
      if (stepProgress >= imageStart && stepProgress < imageEnd) {
        // Zoom out lebih lama (durasi 0.8 porsi step)
        const progress = (stepProgress - imageStart) / 0.8
        opacity = Math.min(progress / 0.2, 1)
        scale = 1.3 - (Math.min(progress, 1) * 0.3)
      }
      
      // Fade out untuk transisi ke slide berikutnya
      if (stepProgress >= index + 0.8) {
        if (index < stepsCount - 1) {
          const fadeOut = (stepProgress - (index + 0.8)) / 0.2
          opacity = Math.max(1 - fadeOut, 0)
        } else {
          // Slide terakhir bertahan sampai benar-benar habis
          opacity = 1
        }
      }
      
      return {
        opacity: opacity,
        transform: `scale(${scale})`,
        zIndex: index
      }
    }
  }
}
</script>

<style scoped lang="scss">
.step-section {
  height: 100vh; /* Hanya setinggi viewport, sisa scroll ditangani ScrollTrigger */
  background: #F8FBFF;
  position: relative;
}

.pin-container {
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* TEXT LAYER */
.step-text-wrapper {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  pointer-events: none;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.step-text {
  font-size: clamp(48px, 10vw, 120px);
  font-weight: 700;
  color: #2E5C8A;
  text-align: center;
  line-height: 1.1;
  padding: 0 40px;
  text-shadow: 0 4px 20px rgba(74, 144, 226, 0.2);
}

/* IMAGE LAYER */
.step-image-wrapper {
  position: absolute;
  inset: 0;
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.image-container {
  width: 100%;
  height: 100%;
  position: relative;
  
  &::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(
      to bottom,
      rgba(74, 144, 226, 0.1) 0%,
      rgba(46, 92, 138, 0.3) 100%
    );
    z-index: 1;
  }
  
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
}

/* Responsive */
@media (max-width: 768px) {
  .step-text {
    font-size: clamp(36px, 12vw, 72px);
    padding: 0 24px;
  }
}

@media (max-width: 480px) {
  .step-text {
    font-size: clamp(32px, 14vw, 56px);
    padding: 0 20px;
  }
}
</style>
