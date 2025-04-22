<script setup lang="ts">
import { onMounted, onBeforeUnmount, ref } from 'vue';
import * as THREE from 'three';

const canvasRef = ref<HTMLCanvasElement | null>(null);
let scene: THREE.Scene;
let camera: THREE.PerspectiveCamera;
let renderer: THREE.WebGLRenderer;
let particles: THREE.Points;
let animationId: number;

onMounted(() => {
  initThree();
  animate();
  
  window.addEventListener('resize', onResize);
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', onResize);
  cancelAnimationFrame(animationId);
  if (renderer) {
    renderer.dispose();
  }
});

function initThree() {
  // Scene setup
  scene = new THREE.Scene();
  
  // Camera setup
  camera = new THREE.PerspectiveCamera(
    75, 
    window.innerWidth / window.innerHeight, 
    0.1, 
    1000
  );
  camera.position.z = 50;
  
  // Renderer setup
  renderer = new THREE.WebGLRenderer({
    canvas: canvasRef.value!,
    alpha: true,
    antialias: true
  });
  renderer.setSize(window.innerWidth, window.innerHeight);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  
  // Create particles
  const particlesGeometry = new THREE.BufferGeometry();
  const count = 2000;
  
  const positions = new Float32Array(count * 3);
  const colors = new Float32Array(count * 3);
  
  const purpleColor = new THREE.Color('#9D4EDD');
  const blueColor = new THREE.Color('#4EA8DE');
  
  for (let i = 0; i < count * 3; i += 3) {
    // Positions
    positions[i] = (Math.random() - 0.5) * 100;
    positions[i + 1] = (Math.random() - 0.5) * 100 - 20;
    positions[i + 2] = (Math.random() - 0.5) * 100;
    
    // Colors - interpolate between purple and blue
    const mixFactor = Math.random();
    const color = new THREE.Color().lerpColors(purpleColor, blueColor, mixFactor);
    
    colors[i] = color.r;
    colors[i + 1] = color.g;
    colors[i + 2] = color.b;
  }
  
  particlesGeometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  particlesGeometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));
  
  // Particles material
  const particlesMaterial = new THREE.PointsMaterial({
    size: 0.5,
    sizeAttenuation: true,
    transparent: true,
    alphaMap: createCircleTexture(),
    depthWrite: false,
    blending: THREE.AdditiveBlending,
    vertexColors: true
  });
  
  particles = new THREE.Points(particlesGeometry, particlesMaterial);
  scene.add(particles);
}

function createCircleTexture() {
  const canvas = document.createElement('canvas');
  canvas.width = 64;
  canvas.height = 64;
  
  const context = canvas.getContext('2d')!;
  context.beginPath();
  context.arc(32, 32, 28, 0, Math.PI * 2);
  context.closePath();
  
  context.fillStyle = 'white';
  context.fill();
  
  const texture = new THREE.CanvasTexture(canvas);
  texture.needsUpdate = true;
  return texture;
}

function animate() {
  animationId = requestAnimationFrame(animate);
  
  if (particles) {
    particles.rotation.x += 0.0003;
    particles.rotation.y += 0.0005;
    
    // Wave motion
    const positions = particles.geometry.attributes.position.array as Float32Array;
    const time = Date.now() * 0.0005;
    
    for (let i = 0; i < positions.length; i += 3) {
      const x = positions[i];
      const y = positions[i + 1];
      
      // Apply subtle wave motion
      positions[i + 1] = y + Math.sin(time + x * 0.1) * 0.1;
    }
    
    particles.geometry.attributes.position.needsUpdate = true;
  }
  
  renderer.render(scene, camera);
}

function onResize() {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
}
</script>

<template>
  <canvas ref="canvasRef" class="particles-canvas"></canvas>
</template>

<style scoped>
.particles-canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
  opacity: 0.5;
}
</style>
