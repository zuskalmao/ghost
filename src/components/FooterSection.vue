<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-logo">
          <img src="/ghost-icon.svg" alt="GhostYield Logo" class="footer-logo-img" />
          <h3 class="logo-text"><span class="gradient-text">Ghost</span>Yield</h3>
        </div>
        
        <div class="footer-links">
          <div class="footer-column">
            <h4>Navigation</h4>
            <a href="#hero">Home</a>
            <a href="#about">About</a>
            <a href="#staking">Staking</a>
          </div>
          
          <div class="footer-column">
            <h4>Resources</h4>
            <a href="#">Whitepaper</a>
            <a href="#">Documentation</a>
            <a href="#">FAQ</a>
          </div>
          
          <div class="footer-column">
            <h4>Community</h4>
            <a href="#">Twitter</a>
            <a href="#">Discord</a>
            <a href="#">Telegram</a>
          </div>
        </div>
      </div>
      
      <div class="footer-bottom">
        <p>&copy; {{ new Date().getFullYear() }} GhostYield. All rights reserved.</p>
        <p>Built with 👻 on Solana</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: var(--bg-dark);
  padding: 4rem 0 2rem;
  position: relative;
  z-index: 10;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 2rem;
  margin-bottom: 3rem;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.footer-logo-img {
  width: 40px;
  height: 40px;
}

.footer-links {
  display: flex;
  gap: 3rem;
  flex-wrap: wrap;
}

.footer-column {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.footer-column h4 {
  color: var(--text-light);
  margin-bottom: 0.5rem;
}

.footer-column a {
  color: var(--text-dim);
  text-decoration: none;
  transition: all 0.3s ease;
}

.footer-column a:hover {
  color: var(--primary-light);
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.footer-bottom p {
  color: var(--text-dim);
  font-size: 0.9rem;
  margin: 0;
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  
  .footer-links {
    width: 100%;
    justify-content: space-around;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
