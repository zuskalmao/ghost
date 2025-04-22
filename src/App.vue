<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import { useWindowScroll } from '@vueuse/core';
import gsap from 'gsap';
import HeroSection from './components/HeroSection.vue';
import AboutSection from './components/AboutSection.vue';
import StakingSection from './components/StakingSection.vue';
import GhostParticles from './components/GhostParticles.vue';
import FooterSection from './components/FooterSection.vue';

const { y } = useWindowScroll();

const isScrolled = computed(() => {
  return y.value > 50;
});

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('show');
      }
    });
  });

  const hiddenElements = document.querySelectorAll('.hidden');
  hiddenElements.forEach((el) => observer.observe(el));

  // Initialize animations
  gsap.from('.logo', {
    y: -50,
    opacity: 0,
    duration: 1.2,
    ease: 'power3.out'
  });

  gsap.from('.nav-link', {
    y: -30,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2,
    ease: 'power3.out'
  });
});
</script>

<template>
  <div class="site-wrapper">
    <header :class="['navbar', { 'scrolled': isScrolled }]">
      <div class="container nav-container">
        <div class="logo-container">
          <img src="/ghost-icon.svg" alt="GhostYield Logo" class="logo" />
          <h3 class="logo-text"><span class="gradient-text">Ghost</span>Yield</h3>
        </div>
        <nav>
          <a href="#hero" class="nav-link">Home</a>
          <a href="#about" class="nav-link">About</a>
          <a href="#staking" class="nav-link">Staking</a>
          <button class="button button-primary connect-wallet">Connect Wallet</button>
        </nav>
      </div>
    </header>

    <GhostParticles />

    <main>
      <HeroSection id="hero" />
      <AboutSection id="about" />
      <StakingSection id="staking" />
    </main>

    <FooterSection />
  </div>
</template>

<style scoped>
.site-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
}

main {
  flex: 1;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 1rem 0;
  transition: all 0.3s ease;
}

.scrolled {
  background: rgba(15, 10, 30, 0.95);
  backdrop-filter: blur(10px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  padding: 0.6rem 0;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo {
  width: 40px;
  height: 40px;
  transition: all 0.3s ease;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 700;
}

nav {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.nav-link {
  color: var(--text);
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  position: relative;
  padding: 0.5rem 0;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, var(--primary) 0%, var(--secondary) 100%);
  transition: all 0.3s ease;
}

.nav-link:hover {
  color: var(--primary-light);
}

.nav-link:hover::after {
  width: 100%;
}

.connect-wallet {
  margin-left: 1rem;
}

/* Responsive styles */
@media (max-width: 768px) {
  nav {
    display: none;
  }
  
  .logo-container {
    margin: 0 auto;
  }
}
</style>
