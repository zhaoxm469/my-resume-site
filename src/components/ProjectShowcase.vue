<script setup lang="ts">
import { ref } from 'vue';

interface Project {
    title: string;
    description: string;
    image: string;
    tags: string[];
    link: string;
}

const projects = ref<Project[]>([
    {
        title: '企业级中台系统',
        description: '基于 Vue3 + TypeScript 的现代化中台解决方案，包含多个子系统和丰富的业务组件',
        image: '/projects/project1.jpg',
        tags: ['Vue3', 'TypeScript', 'Micro-Frontend'],
        link: '#'
    },
    {
        title: '数据可视化平台',
        description: '使用 Three.js 和 ECharts 打造的3D数据可视化解决方案',
        image: '/projects/project2.jpg',
        tags: ['Three.js', 'ECharts', 'WebGL'],
        link: '#'
    },
    {
        title: '跨平台应用框架',
        description: '统一 Web、小程序、App 的开发框架，提升开发效率',
        image: '/projects/project3.jpg',
        tags: ['Hybrid', 'Flutter', 'React Native'],
        link: '#'
    }
]);
</script>

<template>
    <section class="py-20 bg-gray-800">
        <div class="container mx-auto px-4">
            <h2 class="text-5xl font-bold text-center mb-16">
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 to-purple-600">
                    项目展示
                </span>
            </h2>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div v-for="project in projects" :key="project.title"
                    class="cursor-pointer group relative bg-gray-900 rounded-xl overflow-hidden transform hover:scale-105 transition-all duration-500">
                    <div
                        class="absolute inset-0 bg-gradient-to-r from-indigo-500/50 to-purple-600/50 opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                    </div>

                    <img :src="project.image" :alt="project.title" class="w-full h-48 object-cover" />

                    <div class="p-6">
                        <h3 class="text-xl font-bold mb-2 text-white">{{ project.title }}</h3>
                        <p class="text-gray-400 mb-4">{{ project.description }}</p>

                        <div class="flex flex-wrap gap-2 mb-4">
                            <span v-for="tag in project.tags" :key="tag"
                                class="px-3 py-1 text-sm rounded-full bg-indigo-500/20 text-indigo-300">
                                {{ tag }}
                            </span>
                        </div>

                        <a :href="project.link"
                            class="inline-block px-4 py-2 rounded-lg bg-gradient-to-r from-indigo-500 to-purple-600 text-white transform hover:translate-y-[-2px] transition-all duration-300">
                            查看详情
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>