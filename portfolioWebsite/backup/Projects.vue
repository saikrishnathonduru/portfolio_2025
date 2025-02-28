<template>
  <section id="projects" class="py-20 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute top-1/4 -right-1/4 w-96 h-96 bg-purple-200 dark:bg-purple-900/20 rounded-full blur-3xl opacity-30"></div>
      <div class="absolute bottom-1/4 -left-1/4 w-96 h-96 bg-blue-200 dark:bg-blue-900/20 rounded-full blur-3xl opacity-30"></div>
    </div>

    <div class="container mx-auto px-6 relative">
      <h2 class="text-5xl font-bold text-center mb-4 bg-gradient-to-r from-purple-600 via-blue-500 to-purple-600 bg-size-200 animate-gradient-x text-transparent bg-clip-text">
        Projects
      </h2>

      <!-- Category Filter -->
      <div class="flex justify-center flex-wrap gap-4 mb-16">
        <button v-for="category in categories"
                :key="category"
                @click="selectedCategory = category"
                class="relative px-6 py-3 rounded-full transition-all duration-300 transform hover:-translate-y-1 overflow-hidden group"
                :class="[
                  selectedCategory === category
                    ? 'bg-gradient-to-r from-purple-600 to-blue-500 text-white shadow-lg'
                    : 'bg-white dark:bg-gray-800 text-gray-600 dark:text-gray-400 hover:shadow-md'
                ]">
          <span class="relative z-10">{{ category }}</span>
          <div v-if="selectedCategory !== category"
               class="absolute inset-0 bg-gradient-to-r from-purple-600/10 to-blue-500/10 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-500 origin-left">
          </div>
        </button>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="project in filteredProjects" 
             :key="project.title"
             @mouseenter="hoveredProject = project"
             @mouseleave="hoveredProject = null"
             class="group relative bg-white dark:bg-gray-800/50 backdrop-blur-lg rounded-2xl overflow-hidden shadow-lg hover:shadow-xl transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-br opacity-0 group-hover:opacity-10 transition-opacity duration-500"
               :class="project.color"></div>
          
          <div class="aspect-video relative overflow-hidden">
            <img :src="project.image" 
                 :alt="project.title"
                 class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-700">
            <div class="absolute inset-0 bg-gradient-to-t from-black/50 via-black/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
          </div>
          
          <div class="p-8 space-y-6">
            <div class="flex items-center justify-between">
              <h3 class="text-2xl font-semibold text-gray-800 dark:text-white group-hover:text-transparent group-hover:bg-clip-text group-hover:bg-gradient-to-r transition-all duration-300"
                  :class="project.color">
                {{ project.title }}
              </h3>
              <span class="px-4 py-1 text-sm bg-gradient-to-r rounded-full text-white shadow-sm"
                    :class="project.color">
                {{ project.category }}
              </span>
            </div>
            
            <p class="text-gray-600 dark:text-gray-400 line-clamp-2">{{ project.description }}</p>
            
            <div class="flex flex-wrap gap-2">
              <span v-for="tech in project.technologies" 
                    :key="tech"
                    class="px-3 py-1 text-sm bg-gray-100 dark:bg-gray-700/50 text-gray-600 dark:text-gray-400 rounded-full backdrop-blur-sm">
                {{ tech }}
              </span>
            </div>
            
            <div class="flex space-x-4 pt-4">
              <a :href="project.links.demo" 
                 target="_blank"
                 class="flex-1 text-center px-4 py-3 bg-gradient-to-r text-white rounded-xl shadow-sm hover:shadow-md transform hover:-translate-y-1 transition-all duration-300"
                 :class="project.color">
                <span class="flex items-center justify-center">
                  <span>Live Demo</span>
                  <svg class="w-4 h-4 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
                  </svg>
                </span>
              </a>
              <a :href="project.links.github"
                 target="_blank"
                 class="flex-1 text-center px-4 py-3 border-2 rounded-xl hover:bg-gray-50 dark:hover:bg-gray-700/50 transform hover:-translate-y-1 transition-all duration-300 group/btn"
                 :class="[
                   hoveredProject === project ? `border-transparent bg-gradient-to-r ${project.color} text-white` : 'border-gray-300 dark:border-gray-600'
                 ]">
                <span class="flex items-center justify-center">
                  <span>Source Code</span>
                  <svg class="w-4 h-4 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path>
                  </svg>
                </span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const projects = [
  {
    title: 'Custom Dashboards',
    description: 'Developed a machine learning model to predict market trends using historical data and sentiment analysis from social media.',
    technologies: ['PowerBI', 'Dax query', 'Machine Learning'],
    image: '/projects/market-analysis.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/market-analysis'
    },
    category: 'Data Analysis',
    color: 'from-purple-500 to-blue-500'
  },
  {
    title: 'Bilingual Term Extraction',
    description: 'Created a bilingual term extraction tool to identify and manage key terms across multiple languages.',
    technologies: ['spaCy', 'Django', 'HTML', 'CSS','JavaScript', 'PostgreSQL'],
    image: '/projects/term-extraction.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/term-extraction'
    },
    category: 'NLP',
    color: 'from-red-500 to-orange-500'
  },
  {
    title: 'URL Word Count',
    description: 'Built a tool to analyze and count words from URLs for content analysis and SEO optimization.',
    technologies: ['Python', 'Selenium', 'BeautifulSoup','crawl4ai', 'FastAPI', 'Vue.js'],
    image: '/projects/url-wordcount.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/url-wordcount'
    },
    category: 'Web Scraping',
    color: 'from-yellow-500 to-red-500'
  },
  {
    title: 'Customer Segmentation Platform',
    description: 'Built an end-to-end platform for customer segmentation using clustering algorithms and interactive visualizations.',
    technologies: ['scikit-learn', 'PostgreSQL', 'D3.js', 'FastAPI', 'React'],
    image: '/projects/customer-segmentation.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/customer-segmentation'
    },
    category: 'Data Analysis',
    color: 'from-blue-500 to-cyan-500'
  },
  {
    title: 'Chatbot',
    description: 'Developed an AI-powered chatbot for automated customer support and knowledge retrieval.',
    technologies: ['LangChain', 'FastAPI', 'Vue.js', 'OpenAI API','Llama'],
    image: '/projects/chatbot.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/chatbot'
    },
    category: 'AI & NLP',
    color: 'from-purple-500 to-blue-500'
  },
  {
    title: 'AI Translation',
    description: 'Developed a translation system leveraging large language models for high-quality multilingual translation.',
    technologies: ['LLM Models', 'FastAPI', 'Vue.js', 'Open router','Huggingface'],
    image: '/projects/translate-llm.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/translate-llm'
    },
    category: 'AI & NLP',
    color: 'from-green-500 to-teal-500'
  }
]

const categories = ['All', 'Machine Learning', 'Data Analysis', 'NLP']
const selectedCategory = ref('All')
const hoveredProject = ref(null)

const filteredProjects = computed(() => {
  if (selectedCategory.value === 'All') return projects
  return projects.filter(project => project.category === selectedCategory.value)
})
</script>

<style scoped>
.container {
  max-width: 1400px;
}

/* Line Clamp for Description */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Gradient Animation */
@keyframes gradient-x {
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

.animate-gradient-x {
  animation: gradient-x 15s ease infinite;
}

.bg-size-200 {
  background-size: 200% 200%;
}
</style>