<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
import { gsap } from 'gsap';
import * as THREE from 'three';

const canvasRef = ref<HTMLCanvasElement | null>(null);
let scene: THREE.Scene;
let camera: THREE.PerspectiveCamera;
let renderer: THREE.WebGLRenderer;
let particles: THREE.Points;
let animationFrameId: number;

const init = () => {
    scene = new THREE.Scene();
    camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

    renderer = new THREE.WebGLRenderer({
        canvas: canvasRef.value!,
        alpha: true,
        antialias: true,
    });

    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth, window.innerHeight);
    camera.position.z = 30;

    // 创建粒子系统
    const particlesGeometry = new THREE.BufferGeometry();
    const particlesCount = 5000;
    const posArray = new Float32Array(particlesCount * 3);

    for (let i = 0; i < particlesCount * 3; i++) {
        posArray[i] = (Math.random() - 0.5) * 50;
    }

    particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));

    const particlesMaterial = new THREE.PointsMaterial({
        size: 0.005,
        color: 0x6366f1,
        transparent: true,
        blending: THREE.AdditiveBlending,
    });

    particles = new THREE.Points(particlesGeometry, particlesMaterial);
    scene.add(particles);

    // 添加环境光
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
    scene.add(ambientLight);
};

const animate = () => {
    particles.rotation.x += 0.0001;
    particles.rotation.y += 0.0002;

    // 鼠标移动时的视差效果
    const parallaxX = (mouseX - window.innerWidth / 2) * 0.0001;
    const parallaxY = (mouseY - window.innerHeight / 2) * 0.0001;
    particles.rotation.x += parallaxX;
    particles.rotation.y += parallaxY;

    renderer.render(scene, camera);
    animationFrameId = requestAnimationFrame(animate);
};

// 鼠标交互
let mouseX = 0;
let mouseY = 0;

const handleMouseMove = (event: MouseEvent) => {
    mouseX = event.clientX;
    mouseY = event.clientY;
};

const handleResize = () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
};

onMounted(() => {
    init();
    animate();

    window.addEventListener('mousemove', handleMouseMove);
    window.addEventListener('resize', handleResize);

    // 标题动画
    gsap.from('.header-content', {
        y: 100,
        opacity: 0,
        duration: 1.5,
        ease: 'power4.out',
    });
});

onUnmounted(() => {
    window.removeEventListener('mousemove', handleMouseMove);
    window.removeEventListener('resize', handleResize);
    cancelAnimationFrame(animationFrameId);
});
</script>

<template>
    <header class="relative h-screen overflow-hidden">
        <canvas ref="canvasRef" class="absolute inset-0 w-full h-full"></canvas>
        <div class="header-content relative z-10 flex flex-col items-center justify-center h-full text-white">
            <div class="text-center space-y-6 backdrop-blur-sm bg-black/10 p-12 rounded-3xl">
                <h1
                    class="text-7xl font-bold mb-6 text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 via-purple-500 to-pink-500">
                    赵星明
                </h1>
                <p class="text-3xl font-light mb-8">
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-indigo-300 to-purple-400">
                        资深前端开发工程师
                    </span>
                </p>
                <div class="flex space-x-6 justify-center">
                    <!-- <a href="#about" class="group relative px-8 py-3 rounded-full overflow-hidden">
                        <span
                            class="absolute inset-0 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500"></span>
                        <span
                            class="relative text-white group-hover:scale-105 transition-transform duration-300 inline-block">
                            了解更多
                        </span>
                    </a> -->
                    <a href="tel:15810275844"
                        class="group px-8 py-3 rounded-full border-2 border-indigo-400 hover:border-purple-500 transition-colors duration-300">
                        <span class="text-white group-hover:text-purple-400 transition-colors duration-300">
                            联系我
                        </span>
                    </a>
                </div>
            </div>
        </div>
    </header>
</template>

<style scoped>
.header-content {
    animation: float 6s ease-in-out infinite;
}

@keyframes float {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }
}
</style>