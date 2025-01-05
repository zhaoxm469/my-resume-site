<script setup lang="ts">
import { onMounted, ref } from 'vue';
import TagCloud from 'TagCloud';

interface TagCloudOptions {
    radius: number;
    maxSpeed: 'fast' | 'slow' | 'normal' | number;
    initSpeed: 'fast' | 'slow' | 'normal' | number;
    direction: number;
    keep: boolean;
    useContainerInlineStyles: boolean;
    containerClass: string;
    itemClass: string;
}

const container = ref<HTMLElement | null>(null);
const texts = [
    'Vue.js', 'React', 'TypeScript',
    'Node.js', 'Webpack', 'Vite',
    'Three.js', 'WebGL', 'Nginx',
    "Caddy", 'CI/CD',
    'Docker', 'MongoDB',
    'Redis'
];

onMounted(() => {
    if (container.value) {
        TagCloud(container.value, texts, {
            radius: 300,
            maxSpeed: 'fast',
            initSpeed: 'fast',
            direction: 135,
            keep: true,
            useContainerInlineStyles: true,
            containerClass: 'tagcloud',
            itemClass: 'tagcloud--item',
        } as TagCloudOptions);
    }
});
</script>

<template>
    <section class="relative min-h-screen bg-gray-900 py-20">
        <div class="container mx-auto px-4">
            <h2 class="text-5xl font-bold text-center mb-16">
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 to-purple-600">
                    技术栈
                </span>
            </h2>
            <div ref="container" class="tagcloud-container"></div>
        </div>
    </section>
</template>

<style scoped>
.tagcloud-container {
    @apply flex justify-center items-center min-h-[600px];
}

.tagcloud {
    @apply font-bold;
    font-size: 1.5rem;
}

.tagcloud--item {
    @apply text-indigo-400 transition-colors duration-300;
    cursor: pointer;
}

.tagcloud--item:hover {
    @apply text-purple-500;
}
</style>