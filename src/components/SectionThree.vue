<template>
  <section class="thank-you-section">
    <div class="thank-you-content">
      <h1 class="thank-you-text">Terima Kasih</h1>
      <p class="subtitle">Thank You for Choosing Our Pet Shop</p>
    </div>
  </section>
</template>

<script>
export default {
  name: "SectionThree"
}
</script>

<style scoped lang="scss">
.thank-you-section {
  min-height: 100vh;
  background-color: #1e88e5;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 60px 40px;
}

.thank-you-content {
  text-align: center;
  animation: fadeInUp 1s ease-out;
}

.thank-you-text {
  font-size: clamp(56px, 12vw, 120px);
  font-weight: 700;
  color: #FFFFFF;
  margin: 0 0 20px 0;
  line-height: 1.1;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}

.subtitle {
  font-size: clamp(18px, 3vw, 28px);
  color: rgba(255, 255, 255, 0.9);
  margin: 0;
  font-weight: 400;
  letter-spacing: 0.5px;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive */
@media (max-width: 768px) {
  .thank-you-section {
    padding: 40px 30px;
  }
}

@media (max-width: 480px) {
  .thank-you-section {
    padding: 30px 20px;
  }
  
  .subtitle {
    font-size: 16px;
  }
}
</style>
