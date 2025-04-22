<script setup lang="ts">
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

onMounted(() => {
  gsap.from('.about-content', {
    y: 30,
    opacity: 0,
    duration: 1,
    ease: 'power3.out',
    scrollTrigger: {
      trigger: '.about-section',
      start: 'top 80%'
    }
  });
});
</script>

<template>
  <section class="about-section section" id="about">
    <div class="container">
      <div class="about-content hidden">
        <h2>About <span class="gradient-text">GhostYield</span></h2>
        <p>GhostYield ($BOO) is a spectral token on Solana that materializes yield out of thin air. Unlike other memecoins, $BOO has a unique staking mechanism that rewards holders with phantom returns.</p>
        
        <div class="features-grid">
          <div class="feature-card card hidden">
            <h3>Spectral Staking</h3>
            <p>Stake your $BOO tokens and watch as ghostly rewards materialize in your wallet. Our unique staking mechanism offers competitive APY that appears out of nowhere.</p>
          </div>
          
          <div class="feature-card card hidden">
            <h3>Phantom Tokenomics</h3>
            <p>With a total supply of 1 billion $BOO tokens, our deflationary model includes regular token burns that reduce supply while maintaining spectral equilibrium.</p>
          </div>
          
          <div class="feature-card card hidden">
            <h3>Ethereal Community</h3>
            <p>Join our vibrant community of ghost enthusiasts. Together, we're building a haunting ecosystem with real utility and supernatural growth potential.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  background: linear-gradient(180deg, var(--bg-dark) 0%, var(--bg) 100%);
}

.about-content {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.feature-card {
  text-align: left;
  transition-delay: calc(var(--order) * 200ms);
}

.feature-card h3 {
  color: var(--primary-light);
  margin-bottom: 1rem;
}

@media (max-width: 768px) {
  .features-grid {
    grid-template-columns: 1fr;
  }
}
</style>
