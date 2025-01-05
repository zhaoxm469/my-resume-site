<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { gsap } from 'gsap';

interface Skill {
  name: string;
  level: number;
  icon: string;
  color: string;
}

const skills = ref<Skill[]>([
  {
    name: 'Vue.js',
    level: 95,
    icon: '🎯',
    color: 'from-green-400 to-green-600'
  },
  {
    name: 'TypeScript',
    level: 90,
    icon: '💪',
    color: 'from-blue-400 to-blue-600'
  },
  {
    name: 'Node.js',
    level: 85,
    icon: '⚡',
    color: 'from-yellow-400 to-yellow-600'
  },
  {
    name: 'Webpack/Vite',
    level: 88,
    icon: '🛠',
    color: 'from-purple-400 to-purple-600'
  },
  {
    name: 'UI/UX',
    level: 85,
    icon: '🎨',
    color: 'from-pink-400 to-pink-600'
  },
  {
    name: 'DevOps',
    level: 80,
    icon: '🚀',
    color: 'from-red-400 to-red-600'
  }
]);

onMounted(() => {
  gsap.from('.skill-card', {
    opacity: 0,
    y: 50,
    duration: 0.8,
    stagger: 0.2,
    scrollTrigger: {
      trigger: '.skills-section',
      start: 'top 80%',
    },
  });

  gsap.to('.skill-progress', {
    width: 'var(--progress)',
    duration: 1.5,
    ease: 'power2.out',
    scrollTrigger: {
      trigger: '.skills-section',
      start: 'top 80%',
    },
  });
});
</script>

<template>
  <section id="skills" class="skills-section py-20 bg-gray-900">
    <div class="container mx-auto px-4 max-w-5xl">
      <h2 class="text-4xl font-bold mb-12 text-center text-white">
        <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-purple-500">
          技能特长
        </span>
      </h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div v-for="skill in skills" :key="skill.name" 
             class="skill-card bg-gray-800 rounded-xl p-6 transform hover:scale-105 transition-all duration-300">
          <div class="flex items-center mb-4">
            <span class="text-2xl mr-3">{{ skill.icon }}</span>
            <h3 class="text-xl font-semibold text-white">{{ skill.name }}</h3>
          </div>
          
          <div class="h-4 bg-gray-700 rounded-full overflow-hidden">
            <div class="skill-progress h-full rounded-full bg-gradient-to-r"
                 :class="skill.color"
                 :style="{ '--progress': `${skill.level}%` }">
            </div>
          </div>
          <div class="mt-2 text-right text-gray-400">
            {{ skill.level }}%
          </div>
        </div>
      </div>
    </div>
  </section>
</template>