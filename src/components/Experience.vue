<script setup lang="ts">
import { onMounted } from 'vue';
import { gsap } from 'gsap';

const experiences = [
    {
        company: '北京阿拉钉科技有限公司',
        position: '前端开发工程师/小组长',
        period: '2022.02 - 至今',
        achievements: [
            '独立开发了三四个关键模块，提升了系统的功能完备性和用户体验',
            '成功维护和管理了十多个前端项目，确保项目稳定运行和持续优化',
            '通过工具优化，将开发体验提升了300%，热更新速度提升了5倍',
            '开发了超过20个业务组件，提升了开发效率30%，降低了BUG率50%'
        ],
        color: 'from-purple-500 to-pink-500'
    },
    {
        company: '北京牛卡福网络科技有限公司',
        position: '前端开发工程师/小组长',
        period: '2018.05 - 2022.02',
        achievements: [
            '推进私有 NPM 仓库的使用',
            '推进 EasyMock 项目，提高前后端联调效率',
            '推进 Sentry 的使用，监控前端错误和异常',
            '开发 Nucarf-CLI 工具，快速拉取项目模板',
            '连续三年被评为优秀员工'
        ],
        color: 'from-blue-500 to-teal-500'
    },
    {
        company: '广德盛源(北京)信息技术有限公司',
        position: '前端开发工程师',
        period: '2017.05 - 2018.5',
        achievements: [
            '成功将移动端商城项目从多页应用重构为单页应用，用户体验显著提升',
            '高效完成多个日常活动页的开发和维护，确保活动顺利进行'
        ],
        color: 'from-green-500 to-cyan-500'
    }
];

onMounted(() => {
    gsap.set('.experience-card', {
        opacity: 1,
        x: 0
    });
});
</script>

<template>
    <section class="experience-section py-20 bg-gray-800">
        <div class="container mx-auto px-4 max-w-5xl">
            <h2 class="text-4xl font-bold mb-12 text-center text-white">
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-purple-400 to-pink-500">
                    工作经验
                </span>
            </h2>

            <div class="space-y-8">
                <div v-for="(exp, index) in experiences" :key="index"
                    class="experience-card relative bg-gray-900 rounded-xl p-8 shadow-xl transform hover:scale-102 transition-all duration-300">
                    <div class="absolute top-0 left-0 w-2 h-full rounded-l-xl bg-gradient-to-b" :class="exp.color">
                    </div>

                    <div class="ml-4">
                        <div class="flex flex-col md:flex-row md:items-center md:justify-between mb-4">
                            <h3 class="text-2xl font-bold text-transparent bg-clip-text bg-gradient-to-r"
                                :class="exp.color">
                                {{ exp.company }}
                            </h3>
                            <p class="text-gray-400">{{ exp.period }}</p>
                        </div>

                        <p class="text-xl font-semibold mb-4 text-white">{{ exp.position }}</p>

                        <ul class="space-y-3">
                            <li v-for="(achievement, i) in exp.achievements" :key="i"
                                class="flex items-start text-gray-300 hover:text-white transition-colors duration-200">
                                <span class="mr-2 text-gradient" :class="exp.color">▹</span>
                                {{ achievement }}
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>