<template>
  <section id="projects" class="py-24 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute top-1/4 -right-1/4 w-96 h-96 bg-purple-200 dark:bg-purple-900/20 rounded-full blur-3xl opacity-30"></div>
      <div class="absolute bottom-1/4 -left-1/4 w-96 h-96 bg-blue-200 dark:bg-blue-900/20 rounded-full blur-3xl opacity-30"></div>
    </div>

    <div class="container mx-auto px-6 relative">
      <!-- Reduce main heading font size from text-5xl to text-4xl -->
      <h2 class="text-4xl font-bold text-center mb-5 bg-gradient-to-r from-purple-600 via-blue-500 to-purple-600 bg-size-200 animate-gradient-x text-transparent bg-clip-text">
        Projects
      </h2>

      <!-- Category Filter - reduce padding and font size -->
      <div class="flex justify-center flex-wrap gap-3 mb-12">
        <button v-for="category in categories"
                :key="category"
                @click="selectedCategory = category"
                class="relative px-5 py-2 rounded-full transition-all duration-300 transform hover:-translate-y-1 overflow-hidden group text-sm"
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
          
          
          
          <div class="p-6 space-y-4">
            <div class="flex items-center justify-between">
              <!-- Reduce project title from text-2xl to text-xl -->
              <h3 class="text-xl font-semibold text-gray-800 dark:text-white group-hover:text-transparent group-hover:bg-clip-text group-hover:bg-gradient-to-r transition-all duration-300"
                  :class="project.color">
                {{ project.title }}
              </h3>
              <!-- Reduce category badge padding and font size -->
              <span class="px-3 py-0.5 text-xs bg-gradient-to-r rounded-full text-white shadow-sm"
                    :class="project.color">
                {{ project.category }}
              </span>
            </div>
            
            <!-- Reduce description text size -->
            <p class="text-gray-600 dark:text-gray-400 text-sm line-clamp-4">{{ project.description }}</p>
            
            <div class="flex flex-wrap gap-2">
              <!-- Reduce technology tags padding and font size -->
              <span v-for="tech in project.technologies" 
                    :key="tech"
                    class="px-2 py-0.5 text-xs bg-gray-100 dark:bg-gray-700/50 text-gray-600 dark:text-gray-400 rounded-full backdrop-blur-sm">
                {{ tech }}
              </span>
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
    title: 'Dashboards',
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
    color: 'from-blue-500 to-cyan-500'
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
  },
  {
    title: 'Transparent Object Detection Using Tiny YOLO v2',
    description: 'Detecting and classifying transparent cups on a conveyor using Tiny YOLO v2 for real-time robotic pick-and-place systems.',
    technologies: ['YOLO v3', 'Deep learning', 'Tensorflow'],
    image: '/projects/translate-llm.jpg',
    links: {
      demo: 'https://demo.example.com',
      github: 'https://github.com/example/translate-llm'
    },
    category: 'DL',
    color: 'from-green-500 to-teal-500'
  }
]

const categories = ['All', 'AI & NLP', 'Data Analysis', 'NLP', 'Web Scraping', 'DL']
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