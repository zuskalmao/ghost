<script setup lang="ts">
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

onMounted(() => {
  gsap.from('.hero-content', {
    y: 30,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  });
  
  gsap.from('.ghost-logo', { 
    y: 20,
    opacity: 0,
    duration: 1.5,
    ease: 'power3.out',
    delay: 0.5
  });
  
  // Start the animation of floating ghosts
  const ghosts = document.querySelectorAll('.floating-ghost');
  ghosts.forEach((ghost, index) => {
    gsap.to(ghost, {
      y: '-20px',
      duration: 2 + index * 0.5,
      repeat: -1,
      yoyo: true,
      ease: 'power1.inOut'
    });
  });
});
</script>

<template>
  <section class="hero-section" id="hero">
    <div class="container hero-container">
      <div class="hero-content">
        <h1>
          <span class="gradient-text">Ghost</span>Yield
          <span class="ticker">$BOO</span>
        </h1>
        <p class="hero-subtitle">The Solana memecoin where the yield appears out of nowhere</p>
        <div class="hero-cta">
          <button class="button button-primary">Buy $BOO</button>
          <button class="button button-secondary">Stake Now</button>
        </div>
      </div>
      
      <div class="ghost-logo">
        <img src="/ghost-icon.svg" alt="GhostYield Logo" class="main-ghost glow" />
        
        <!-- Floating mini ghosts -->
        <div class="floating-ghost ghost-1">👻</div>
        <div class="floating-ghost ghost-2">👻</div>
        <div class="floating-ghost ghost-3">👻</div>
      </div>
    </div>
    
    <div class="hero-bg"></div>
  </section>
</template>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding-top: 5rem;
  overflow: hidden;
}

.hero-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  z-index: 2;
}

.hero-content {
  max-width: 50%;
}

.hero-subtitle {
  font-size: clamp(1.1rem, 1.8vw, 1.8rem);
  margin-bottom: 2.5rem;
  color: var(--text-light);
}

.hero-cta {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

.ticker {
  font-size: 0.6em;
  background: rgba(255, 255, 255, 0.1);
  padding: 0.2em 0.5em;
  border-radius: 8px;
  margin-left: 0.5rem;
  vertical-align: middle;
  color: var(--primary-light);
}

.ghost-logo {
  position: relative;
  width: 40%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main-ghost {
  width: 100%;
  max-width: 300px;
  animation: pulse 3s infinite ease-in-out;
}

.floating-ghost {
  position: absolute;
  font-size: 2rem;
  animation: float 5s infinite ease-in-out;
  filter: drop-shadow(0 0 5px var(--primary-light));
  opacity: 0.8;
}

.ghost-1 {
  top: 20%;
  left: 10%;
  animation-delay: 0.5s;
  font-size: 1.5rem;
}

.ghost-2 {
  bottom: 30%;
  right: 15%;
  animation-delay: 1s;
  font-size: 2rem;
}

.ghost-3 {
  top: 60%;
  left: 20%;
  animation-delay: 1.5s;
  font-size: 1.8rem;
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at 50% 50%, rgba(157, 78, 221, 0.2) 0%, rgba(15, 10, 30, 0) 70%);
  z-index: 1;
}

@media (max-width: 1024px) {
  .hero-container {
    flex-direction: column;
    text-align: center;
    gap: 3rem;
  }
  
  .hero-content {
    max-width: 100%;
  }
  
  .hero-cta {
    justify-content: center;
  }
}
</style>
