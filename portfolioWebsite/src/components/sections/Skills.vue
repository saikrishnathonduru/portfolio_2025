<template>
  <section id="skills" class="py-20 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute top-1/4 -right-1/4 w-96 h-96 bg-purple-200 dark:bg-purple-900/20 rounded-full blur-3xl opacity-30"></div>
      <div class="absolute bottom-1/4 -left-1/4 w-96 h-96 bg-blue-200 dark:bg-blue-900/20 rounded-full blur-3xl opacity-30"></div>
    </div>

    <div class="container mx-auto px-4 relative">
      <h2 class="text-4xl font-bold text-center mb-4 bg-gradient-to-r from-purple-600 to-blue-500 text-transparent bg-clip-text">
        Skills
      </h2>
      <p class="text-gray-600 dark:text-gray-400 text-center mb-16">My Technical Expertise</p>
      
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div v-for="(categorySkills, category) in skills" 
             :key="category" 
             class="bg-white dark:bg-gray-800 rounded-2xl p-8 shadow-lg hover:shadow-xl transition-all duration-300 transform hover:-translate-y-1">
          <h3 class="text-2xl font-semibold mb-8 text-center bg-gradient-to-r from-purple-600 to-blue-500 text-transparent bg-clip-text">
            {{ category }}
          </h3>
          <div class="space-y-6">
            <div v-for="skill in categorySkills" 
                 :key="skill.name"
                 class="group">
              <div class="flex items-center space-x-4 mb-2">
                <span class="text-2xl transform group-hover:scale-110 transition-transform duration-300">
                  {{ skill.icon }}
                </span>
                <div class="flex-1">
                  <div class="flex justify-between items-center">
                    <span class="font-medium text-gray-800 dark:text-gray-200">{{ skill.name }}</span>
                    <span class="text-sm text-gray-500 dark:text-gray-400">{{ skill.level }}</span>
                  </div>
                </div>
              </div>
              <div class="h-2 bg-gray-200 dark:bg-gray-700 rounded-full overflow-hidden">
                <div class="h-full bg-gradient-to-r from-purple-600 to-blue-500 rounded-full transform origin-left transition-transform duration-1000 ease-out"
                     :style="{ transform: `scaleX(${skill.progress / 100})` }"></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = {
  'Data Science': [
    { name: 'Python', level: 'Experienced', icon: '🐍', progress: 90 },
    { name: 'Machine Learning', level: 'Experienced', icon: '🤖', progress: 85 },
    { name: 'Deep Learning', level: 'Intermediate', icon: '🧠', progress: 75 },
    { name: 'Data Visualization', level: 'Experienced', icon: '📊', progress: 90 },
    { name: 'Statistical Analysis', level: 'Experienced', icon: '📈', progress: 85 },
    { name: 'Natural Language Processing', level: 'Intermediate', icon: '📝', progress: 70 }
  ],
  'Frontend Development': [
    { name: 'Vue.js', level: 'Experienced', icon: '⚡', progress: 90 },
    { name: 'JavaScript/TypeScript', level: 'Experienced', icon: '💻', progress: 85 },
    { name: 'HTML/CSS', level: 'Experienced', icon: '🎨', progress: 90 },
    { name: 'Tailwind CSS', level: 'Intermediate', icon: '🎯', progress: 80 },
    { name: 'React', level: 'Intermediate', icon: '⚛️', progress: 75 }
  ],
  'Backend & DevOps': [
    { name: 'FastAPI', level: 'Experienced', icon: '🚀', progress: 85 },
    { name: 'PostgreSQL', level: 'Experienced', icon: '🐘', progress: 85 },
    { name: 'Docker', level: 'Intermediate', icon: '🐳', progress: 75 },
    { name: 'AWS', level: 'Intermediate', icon: '☁️', progress: 70 },
    { name: 'Git', level: 'Experienced', icon: '📦', progress: 90 }
  ]
}
</script>

<style scoped>
.container {
  max-width: 1200px;
}

/* Hover Effect for Skill Cards */
.group:hover .h-2 > div {
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
  100% {
    opacity: 1;
  }
}
</style>