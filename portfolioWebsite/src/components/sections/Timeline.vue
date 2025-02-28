<template>
  <section id="timeline" class="py-20 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute top-1/4 -right-1/4 w-96 h-96 bg-purple-200 dark:bg-purple-900/20 rounded-full blur-3xl opacity-30"></div>
      <div class="absolute bottom-1/4 -left-1/4 w-96 h-96 bg-blue-200 dark:bg-blue-900/20 rounded-full blur-3xl opacity-30"></div>
    </div>

    <div class="container mx-auto px-4 relative">
      <h2 class="text-4xl font-bold text-center mb-4 bg-gradient-to-r from-purple-600 to-blue-500 text-transparent bg-clip-text">
        Experience
      </h2>
      <p class="text-gray-600 dark:text-gray-400 text-center mb-16">My Professional Journey</p>

      <div class="relative max-w-4xl mx-auto">
        <!-- Timeline Line -->
        <div class="absolute left-1/2 transform -translate-x-px h-full w-0.5 bg-gradient-to-b from-purple-600 to-blue-500 opacity-50"></div>

        <!-- Timeline Items -->
        <div class="space-y-16">
          <div v-for="(exp, index) in experiences" 
               :key="index"
               :data-index="index"
               class="timeline-item relative"
               :class="{ 'opacity-100 translate-y-0': isVisible[index], 'opacity-0 translate-y-8': !isVisible[index] }"
               style="transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1)">
            <!-- Timeline Dot -->
            <div class="absolute left-1/2 transform -translate-x-1/2 -translate-y-4">
              <div class="w-8 h-8 rounded-full border-4 border-purple-600 dark:border-purple-400 bg-white dark:bg-gray-800 shadow-lg"></div>
            </div>

            <!-- Content -->
            <div class="relative flex items-center justify-between">
              <!-- Period -->
              <div class="w-5/12 text-right pr-8">
                <span class="text-purple-600 dark:text-purple-400 font-semibold">{{ exp.period }}</span>
              </div>

              <!-- Details -->
              <div class="w-5/12 pl-8">
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 transform hover:-translate-y-1">
                  <h3 class="text-xl font-semibold mb-2 text-gray-800 dark:text-white">{{ exp.role }}</h3>
                  <p class="text-purple-600 dark:text-purple-400 font-medium mb-3">{{ exp.company }}</p>
                  <p class="text-gray-600 dark:text-gray-400 mb-4">{{ exp.description }}</p>
                  <ul class="space-y-2">
                    <li v-for="achievement in exp.achievements" 
                        :key="achievement"
                        class="flex items-center text-sm text-gray-600 dark:text-gray-400">
                      <span class="mr-2 text-purple-600 dark:text-purple-400">▹</span>
                      {{ achievement }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const experiences = [
  {
    period: '2023 - Present',
    role: 'Senior Data Scientist',
    company: 'Tech Innovation Labs',
    description: 'Lead data scientist responsible for developing and deploying machine learning models for predictive analytics and natural language processing.',
    achievements: [
      'Developed an AI-powered market analysis platform',
      'Led a team of 3 data scientists',
      'Reduced model training time by 40%'
    ]
  },
  {
    period: '2021 - 2023',
    role: 'Data Scientist & Full-Stack Developer',
    company: 'Data Solutions Inc.',
    description: 'Combined data science and full-stack development skills to create end-to-end data solutions and interactive dashboards.',
    achievements: [
      'Built real-time data processing pipeline',
      'Implemented customer segmentation platform',
      'Improved application performance by 60%'
    ]
  },
  {
    period: '2020 - 2021',
    role: 'Junior Data Scientist',
    company: 'AI Startups Co.',
    description: 'Started career in data science, focusing on machine learning model development and data analysis.',
    achievements: [
      'Developed classification algorithms',
      'Created automated reporting system',
      'Optimized ETL processes'
    ]
  }
]

const isVisible = ref(new Array(experiences.length).fill(false))

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const index = parseInt(entry.target.dataset.index)
        isVisible.value[index] = true
      }
    })
  }, { threshold: 0.2 })

  document.querySelectorAll('.timeline-item').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<style scoped>
.container {
  max-width: 1200px;
}

/* Timeline Line Gradient Animation */
@keyframes gradient-flow {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.timeline-line {
  background: linear-gradient(to bottom, #9333ea, #3b82f6);
  background-size: 200% 200%;
  animation: gradient-flow 6s ease infinite;
}
</style>