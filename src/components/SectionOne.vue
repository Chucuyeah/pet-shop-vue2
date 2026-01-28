<template>
  <section class="scroll-section" ref="scrollSection">
    
    <!-- Content Container -->
    <div class="scroll-container">
      
      <!-- Left Side - Text Content (Desktop) / Full Content (Mobile) -->
      <div class="text-content">
        <div 
          v-for="(content, index) in textContents" 
          :key="index"
          class="content-block"
          :ref="`content-${index}`"
          :id="content.id"
        >
          <!-- Icon -->
          <div class="content-icon">{{ icons[index] }}</div>
          
          <h2 class="content-title">{{ content.title }}</h2>
          <p class="content-description">{{ content.description }}</p>
          
          <!-- Image inline for mobile/tablet -->
          <div class="inline-image">
            <img :src="images[index]" :alt="content.title" />
          </div>
        </div>
      </div>

      <!-- Right Side - Sticky Image Container (Desktop only) -->
      <div class="image-container">
        <div class="sticky-wrapper">
          <div class="image-stack">
            <div 
              v-for="(image, index) in images" 
              :key="index"
              class="image-item"
              :class="{ active: activeImageIndex === index }"
            >
              <img :src="image" :alt="textContents[index].title" />
            </div>
          </div>
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
  name: "SectionOne",

  data() {
    return {
      activeImageIndex: 0,
      images: [
        require("@/assets/images/grooming.jpeg"),
        require("@/assets/images/food.jpeg"),
        require("@/assets/images/clinic.jpeg")
      ],
       icons: ["🐶", "🍖", "🏥"],
      textContents: [
        {
          id: "grooming",
          title: "Pet Grooming Services",
          description: "Professional grooming services to keep your pets looking and feeling their best. Our experienced groomers provide gentle care with premium products, ensuring your furry friends are clean, comfortable, and stylish."
        },
        {
          id: "food",
          title: "Healthy Pet Food",
          description: "Nutritious and delicious food options specially formulated for your pet's health. We offer premium brands and custom meal plans that support optimal growth, energy, and wellbeing for pets of all ages and breeds."
        },
        {
          id: "clinic",
          title: "Veterinary Clinic",
          description: "Complete healthcare solutions from preventive care to emergency services. Our certified veterinarians use state-of-the-art equipment to diagnose and treat your pets, ensuring they live long, healthy, and happy lives."
        }
      ]
    }
  },

  mounted() {
    this.initScrollAnimations()
  },

  methods: {
    initScrollAnimations() {
      const contentBlocks = this.$el.querySelectorAll(".content-block")
      
      contentBlocks.forEach((block, index) => {
        ScrollTrigger.create({
          trigger: block,
          start: "top center",
          end: "bottom center",
          onEnter: () => this.changeImage(index),
          onEnterBack: () => this.changeImage(index),
          onUpdate: (self) => {
            // Update header based on scroll progress
            if (this.$parent.$refs && this.$parent.$refs.headerRef) {
              const header = this.$parent.$refs.headerRef
              if (header && header.setActiveWord) {
                header.setActiveWord(index)
              }
            }
          }
        })
      })

      ScrollTrigger.create({
        trigger: this.$el,
        start: "top top",
        end: "bottom bottom",
        pin: this.$el.querySelector(".sticky-wrapper"),
        pinSpacing: false
      })
    },

    changeImage(index) {
      this.activeImageIndex = index
    }
  }
}
</script>

<style lang="scss" scoped>
.scroll-section {
  position: relative;
  background: #F8FBFF;
  padding: 80px 0;
}

/* Container */
.scroll-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 60px;
  display: flex;
  gap: 80px;
  align-items: flex-start;
}

/* Text Content - Left Side */
.text-content {
  flex: 1;
  width: 50%;
}

.content-block {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 60px 0;
}

.content-icon {
  font-size: 72px;
  margin-bottom: 30px;
  line-height: 1;
  
  /* Add subtle animation */
  animation: iconFloat 3s ease-in-out infinite;
}

@keyframes iconFloat {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.content-title {
  font-size: clamp(36px, 5vw, 52px);
  font-weight: 600;
  line-height: 1.2;
  color: #2E5C8A;
  margin: 0 0 24px 0;
}

.content-description {
  font-size: 17px;
  line-height: 1.7;
  color: #555;
  max-width: 540px;
  margin: 0;
}

/* Image Container - Right Side (Sticky) */
.image-container {
  flex: 1;
  width: 60%;
  position: relative;
}

.sticky-wrapper {
  position: sticky;
  top: 120px;
  height: calc(100vh - 240px);
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-stack {
  position: relative;
  width: 100%;
  height: 100%;
  max-width: 600px;
  max-height: 700px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(74, 144, 226, 0.15);
}

.image-item {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transform: scale(1.05);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);

  &.active {
    opacity: 1;
    transform: scale(1);
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
}

/* Inline Image (Mobile/Tablet only) */
.inline-image {
  display: none; /* Hidden on desktop */
  width: 100%;
  margin-top: 30px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(74, 144, 226, 0.15);
  
  img {
    width: 100%;
    height: auto;
    display: block;
    object-fit: cover;
  }
}

/* Responsive */

/* Tablet - Landscape */
@media (max-width: 1200px) and (min-width: 1025px) {
  .scroll-container {
    padding: 0 50px;
    gap: 60px;
  }

  .text-content {
    width: 45%;
  }

  .image-container {
    width: 55%;
  }

  .content-title {
    font-size: 44px;
  }

  .content-description {
    font-size: 16px;
  }

  .sticky-wrapper {
    top: 100px;
    height: calc(100vh - 200px);
  }

  .image-stack {
    max-width: 500px;
    max-height: 600px;
  }
}

/* Tablet - Portrait */
@media (max-width: 1024px) {
  .scroll-section {
    padding: 60px 0;
  }

  .scroll-container {
    flex-direction: column;
    gap: 0;
    padding: 0 40px;
  }

  .text-content {
    width: 100%;
  }

  /* Hide desktop sticky image container */
  .image-container {
    display: none;
  }

  /* Show inline images */
  .inline-image {
    display: block;
    height: 400px;
    border-radius: 20px;
    margin-top: 30px;
    margin-bottom: 50px;
    
    img {
      height: 100%;
      object-fit: cover;
      border-radius: 20px;
    }
  }

  .content-block {
    min-height: auto;
    padding: 40px 0 0;
  }

  .content-icon {
    font-size: 60px;
    margin-bottom: 24px;
  }

  .content-title {
    font-size: 38px;
    margin-bottom: 20px;
  }

  .content-description {
    font-size: 16px;
    line-height: 1.6;
    max-width: 100%;
  }
}

/* Mobile - Large */
@media (max-width: 768px) {
  .scroll-section {
    padding: 40px 0;
  }

  .scroll-container {
    padding: 0 24px;
  }

  .inline-image {
    height: 350px;
    border-radius: 16px;
    margin-top: 25px;
    margin-bottom: 40px;
    
    img {
      border-radius: 16px;
    }
  }

  .content-block {
    padding: 30px 0 0;
  }

  .content-icon {
    font-size: 52px;
    margin-bottom: 20px;
  }

  .content-title {
    font-size: 32px;
    margin-bottom: 16px;
  }

  .content-description {
    font-size: 15px;
    line-height: 1.65;
  }
}

/* Mobile - Small */
@media (max-width: 480px) {
  .scroll-section {
    padding: 30px 0;
  }

  .scroll-container {
    padding: 0 20px;
  }

  .inline-image {
    height: 300px;
    border-radius: 12px;
    margin-top: 20px;
    margin-bottom: 30px;
    box-shadow: 0 10px 40px rgba(74, 144, 226, 0.12);
    
    img {
      border-radius: 12px;
    }
  }

  .content-block {
    padding: 25px 0 0;
  }

  .content-icon {
    font-size: 48px;
    margin-bottom: 18px;
  }

  .content-title {
    font-size: 28px;
    margin-bottom: 14px;
  }

  .content-description {
    font-size: 14px;
    line-height: 1.7;
  }
}/* Center Icon */
.center-icon {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 140px;
  color: #510cffff;
  pointer-events: none;
  z-index: 5;

  @media (max-width: 768px) {
    font-size: 100px;
  }

  @media (max-width: 480px) {
    font-size: 80px;
  }
}

</style>
