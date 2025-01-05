<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue';

interface Particle {
  x: number;
  y: number;
  size: number;
  speedX: number;
  speedY: number;
}

const particles: Particle[] = [];
let canvas: HTMLCanvasElement;
let ctx: CanvasRenderingContext2D;
let animationFrame: number;

const createParticle = (x: number, y: number): Particle => ({
  x,
  y,
  size: Math.random() * 3 + 1,
  speedX: Math.random() * 2 - 1,
  speedY: Math.random() * 2 - 1
});

const initParticles = () => {
  for (let i = 0; i < 50; i++) {
    particles.push(createParticle(
      Math.random() * window.innerWidth,
      Math.random() * window.innerHeight
    ));
  }
};

const animate = () => {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  
  particles.forEach(particle => {
    particle.x += particle.speedX;
    particle.y += particle.speedY;
    
    if (particle.x > canvas.width) particle.x = 0;
    if (particle.x < 0) particle.x = canvas.width;
    if (particle.y > canvas.height) particle.y = 0;
    if (particle.y < 0) particle.y = canvas.height;
    
    ctx.beginPath();
    ctx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(255, 255, 255, 0.5)';
    ctx.fill();
  });
  
  animationFrame = requestAnimationFrame(animate);
};

const handleResize = () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
};

onMounted(() => {
  canvas = document.querySelector('#particleCanvas')!;
  ctx = canvas.getContext('2d')!;
  
  handleResize();
  window.addEventListener('resize', handleResize);
  
  initParticles();
  animate();
});

onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
  cancelAnimationFrame(animationFrame);
});
</script>

<template>
  <canvas id="particleCanvas" class="fixed top-0 left-0 w-full h-full pointer-events-none"></canvas>
</template>