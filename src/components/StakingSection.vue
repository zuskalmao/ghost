<script setup lang="ts">
import { ref, computed } from 'vue';

const stakedAmount = ref(0);
const stakingDuration = ref(30); // days
const apy = ref(69.42); // nice

const estimatedRewards = computed(() => {
  return (stakedAmount.value * apy.value / 100) * (stakingDuration.value / 365);
});

const handleStake = () => {
  alert('Wallet connection required to stake $BOO tokens');
};
</script>

<template>
  <section class="staking-section section" id="staking">
    <div class="container">
      <div class="staking-content hidden">
        <h2>Stake Your <span class="gradient-text">$BOO</span></h2>
        <p>Earn spectral rewards by staking your $BOO tokens. Our ghostly staking mechanism offers competitive APY that materializes out of thin air.</p>
        
        <div class="staking-card card">
          <div class="staking-info">
            <div class="info-item">
              <h4>Current APY</h4>
              <p class="highlight">{{ apy }}%</p>
            </div>
            <div class="info-item">
              <h4>Total Staked</h4>
              <p>142,857,123 $BOO</p>
            </div>
            <div class="info-item">
              <h4>Stakers</h4>
              <p>1,337</p>
            </div>
          </div>
          
          <div class="staking-calculator">
            <h3>Rewards Calculator</h3>
            <div class="input-group">
              <label for="staked-amount">Amount to Stake</label>
              <input 
                type="number" 
                id="staked-amount" 
                v-model="stakedAmount" 
                placeholder="Enter $BOO amount"
              />
            </div>
            
            <div class="input-group">
              <label for="staking-duration">Staking Period (days)</label>
              <input 
                type="range" 
                id="staking-duration" 
                v-model="stakingDuration" 
                min="1" 
                max="365"
              />
              <span>{{ stakingDuration }} days</span>
            </div>
            
            <div class="rewards-estimate">
              <h4>Estimated Rewards</h4>
              <p class="gradient-text">{{ estimatedRewards.toFixed(2) }} $BOO</p>
            </div>
            
            <button class="button button-primary" @click="handleStake">Stake Now</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.staking-section {
  background: linear-gradient(180deg, var(--bg) 0%, var(--bg-dark) 100%);
}

.staking-content {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.staking-card {
  margin-top: 3rem;
  padding: 2.5rem;
}

.staking-info {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 2rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.info-item h4 {
  color: var(--text-dim);
  margin-bottom: 0.5rem;
  font-size: 1rem;
}

.info-item p {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0;
}

.staking-calculator {
  max-width: 500px;
  margin: 0 auto;
}

.staking-calculator h3 {
  margin-bottom: 1.5rem;
  color: var(--primary-light);
}

.input-group {
  margin-bottom: 1.5rem;
  text-align: left;
}

.input-group label {
  display: block;
  margin-bottom: 0.5rem;
  color: var(--text-light);
}

.input-group input {
  width: 100%;
}

.input-group span {
  display: block;
  text-align: right;
  margin-top: 0.5rem;
  color: var(--text-dim);
}

.rewards-estimate {
  margin: 2rem 0;
  padding: 1rem;
  background: rgba(157, 78, 221, 0.1);
  border-radius: 8px;
}

.rewards-estimate h4 {
  margin-bottom: 0.5rem;
  color: var(--text-light);
}

.rewards-estimate p {
  font-size: 2rem;
  font-weight: 700;
  margin: 0;
}

@media (max-width: 768px) {
  .staking-info {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
</style>
