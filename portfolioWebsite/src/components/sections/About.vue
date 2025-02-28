<template>
  <section id="about" class="py-24 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 bg-gradient-to-br from-white via-orange-50/30 to-white"></div>
    <div class="absolute top-0 left-0 w-full h-full bg-grid-pattern opacity-5"></div>
    <div class="absolute top-20 -left-32 w-80 h-80 bg-primary/10 rounded-full filter blur-3xl animate-pulse"></div>
    <div class="absolute bottom-20 -right-32 w-80 h-80 bg-secondary/10 rounded-full filter blur-3xl animate-pulse" style="animation-delay: 2s;"></div>

    <div class="container mx-auto px-4 relative">
      <!-- Section Header -->
      <div class="text-center mb-8">
        <h2 class="text-3xl font-bold mb-2 bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent 
                   animate-fade-in-up">About Me</h2>
        <div class="w-16 h-1 bg-gradient-to-r from-primary to-secondary mx-auto rounded-full"></div>
      </div>

      <!-- Introduction -->
      <div class="prose prose-base mx-auto text-center max-w-4xl mb-8 relative">
        <!-- Decorative Elements -->
        <div class="absolute -left-4 top-1/2 w-6 h-6 bg-primary/10 rounded-full animate-float"></div>
        <div class="absolute -right-4 top-1/3 w-4 h-4 bg-secondary/10 rounded-full animate-float" style="animation-delay: 1s;"></div>
        
        <div class="p-6 bg-white/40 backdrop-blur-lg rounded-2xl shadow-xl hover:shadow-2xl 
                    transition-all duration-500 border border-white/20 group">
          <div class="space-y-4">
            <p class="text-gray-700 leading-relaxed text-sm md:text-base">
              Specialized in AI-driven solutions, with expertise in <span class="text-primary font-medium">LLMs, RAG-powered retrieval systems, and multilingual NLP applications</span>. 
              Experience spans across architecting scalable <span class="text-primary font-medium">data pipelines, AI automation, and predictive business intelligence</span>, enabling enterprises to make data-driven decisions.
            </p>
            <p class="text-gray-700 leading-relaxed text-sm md:text-base">
              Adept at integrating <span class="text-primary font-medium">MLOps best practices, cloud-native technologies</span> (AWS, GCP, Azure), and frameworks like PyTorch and Hugging Face 
              to deliver <span class="text-primary font-medium">production-grade AI systems</span>.
            </p>
            <p class="text-gray-700 leading-relaxed text-sm md:text-base">
              Currently focused on developing an <span class="text-primary font-medium">AI-powered MVP</span>, bridging <span class="text-primary font-medium">automation and intelligent decision-making</span>. 
              Exploring its <span class="text-primary font-medium">market viability</span>, refining performance, and ensuring <span class="text-primary font-medium">scalability</span> for enterprise use cases.
            </p>
            <p class="text-gray-700 leading-relaxed text-sm md:text-base">
              Passionate about building <span class="text-primary font-medium">AI solutions</span> that enhance <span class="text-primary font-medium">efficiency, adaptability, and real-world impact</span>. 
              Open to <span class="text-primary font-medium">collaborations, discussions, and exploring cutting-edge AI innovations</span>.
            </p>
          </div>
        </div>
      </div>

      <!-- Three Column Layout -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Expertise Section -->
        <div class="group">
          <div class="bg-white/40 backdrop-blur-lg rounded-2xl p-6 shadow-lg border border-white/20 
                      hover:shadow-xl transition-all duration-500 h-full relative overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-br from-primary/5 to-transparent opacity-0 
                        group-hover:opacity-100 transition-opacity duration-500"></div>
            <h3 class="text-xl font-semibold mb-4 text-primary text-center relative">
              Expertise & Tech Stack
              <div class="w-12 h-0.5 bg-primary/30 mx-auto mt-2 group-hover:w-20 transition-all duration-500"></div>
            </h3>
            <div class="space-y-4 relative">
              <!-- Core Expertise -->
              <div>
                <h4 class="text-lg font-medium text-gray-700 mb-2">Core Skills</h4>
                <div class="flex flex-wrap justify-center gap-2">
                  <span v-for="skill in expertise" 
                        :key="skill"
                        class="badge badge-primary badge-sm transform hover:scale-110 hover:rotate-1 transition-all duration-300">
                    {{ skill }}
                  </span>
                </div>
              </div>
              <!-- Tech Stack -->
              <div>
                <h4 class="text-lg font-medium text-gray-700 mb-2">Technologies</h4>
                <div class="flex flex-wrap justify-center gap-2">
                  <span v-for="tech in techStack" 
                        :key="tech"
                        class="badge badge-secondary badge-sm transform hover:scale-110 hover:rotate-1 transition-all duration-300">
                    {{ tech }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Education Section -->
        <div class="group">
          <div class="bg-white/40 backdrop-blur-lg rounded-2xl p-6 shadow-lg border border-white/20 
                      hover:shadow-xl transition-all duration-500 h-full relative overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-br from-primary/5 to-transparent opacity-0 
                        group-hover:opacity-100 transition-opacity duration-500"></div>
            <h3 class="text-xl font-semibold mb-4 text-primary text-center relative">
              Education
              <div class="w-12 h-0.5 bg-primary/30 mx-auto mt-2 group-hover:w-20 transition-all duration-500"></div>
            </h3>
            <div class="space-y-4 relative">
              <div v-for="edu in education" 
                   :key="edu.degree"
                   class="p-3 bg-white/50 rounded-xl hover:bg-white/70 transition-all duration-300
                          transform hover:scale-105 hover:shadow-md">
                <div class="flex justify-between items-center mb-1">
                  <h4 class="font-medium text-base text-gray-800">{{ edu.degree }}</h4>
                  <span class="px-2 py-0.5 bg-primary/10 text-primary text-xs rounded-full ml-2">{{ edu.year }}</span>
                </div>
                <p class="text-gray-600 text-sm">{{ edu.field }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Experience Section -->
        <div class="group">
          <div class="bg-white/40 backdrop-blur-lg rounded-2xl p-6 shadow-lg border border-white/20 
                      hover:shadow-xl transition-all duration-500 h-full relative overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-br from-primary/5 to-transparent opacity-0 
                        group-hover:opacity-100 transition-opacity duration-500"></div>
            <h3 class="text-xl font-semibold mb-4 text-primary text-center relative">
              Experience
              <div class="w-12 h-0.5 bg-primary/30 mx-auto mt-2 group-hover:w-20 transition-all duration-500"></div>
            </h3>
            <div class="space-y-4">
              <div v-for="(exp, index) in experience" :key="index" class="relative bg-white/50 rounded-xl hover:bg-white/70 transition-all duration-300
                          transform hover:scale-105 hover:shadow-md">
                <div class="flex items-start space-x-2">
                  <div class="w-2 h-2 bg-primary rounded-full mt-2 flex-shrink-0"></div>
                  <div>
                    <h4 class="text-sm font-semibold text-gray-800">{{ exp.role }}</h4>
                    <p class="text-xs text-gray-600">{{ exp.company }} | {{ exp.period }}</p>
                    <p class="text-xs text-gray-700 mt-1">{{ exp.description }}</p>
                  </div>
                </div>
                <div v-if="index < experience.length - 1" class="w-0.5 h-4 bg-primary/20 ml-1 my-1"></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const expertise = [
  'AI/ML/DL/NLP',
  'LLMs & RAG Systems',
  'LLMOps',
  'Data Engineering',
  'Agentic Workflow Automation',
  'Fine-Tuning LLMs', 'ETL',
  'Business Intelligence'
];

const techStack = [
  'Python','PyTorch', 'TensorFlow',
  'AWS', 'Azure', 'Qdrant','PowerBI','Git','Crawl4AI',
  'FastAPI', 'Django', 'LangChain','HuggingFace',
  'PostgreSQL', 'MySQL','HTML', 'CSS','JavaScript',
  'Vue.js', 'Element-Plus','tailwind css','AGNO', 'n8n'
];

const education = [
  {
    degree: 'M.Sc. Engineering',
    field: 'Automation Technology',
    year: '2020'
  },
  {
    degree: 'B.Sc. Engineering',
    field: 'Mechanical Engineering',
    year: '2016'
  }
];

const experience = [
  {
    role: 'Full-Stack Data Scientist',
    company: 'Kern AG',
    period: '2023 - Present',
    description: 'Leading AI product development, focusing on LLMs and RAG systems.'
  },
  {
    role: 'Machine Learning and Systems Engineer',
    company: 'Kern AG',
    period: '2021 - 2023',
    description: 'Architected scalable ML pipelines and data-driven BI solutions.'
  },
  {
    role: 'Machine Learning Freelancer',
    company: ' Rawskill',
    period: '2021 - 2021',
    description: 'Engineered OCR system for virtual football utilizing Tesseract and image enhancement techniques.'
  }
];
</script>

<style scoped>
.badge {
  @apply px-3 py-1.5 text-xs font-medium;
}

.badge-sm {
  @apply hover:shadow-sm cursor-default;
}

.container {
  max-width: 1400px;
}

.bg-grid-pattern {
  background-image: linear-gradient(to right, rgb(var(--primary-rgb) / 0.1) 1px, transparent 1px),
    linear-gradient(to bottom, rgb(var(--primary-rgb) / 0.1) 1px, transparent 1px);
  background-size: 4rem 4rem;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-float {
  animation: float 6s ease-in-out infinite;
}

.animate-fade-in-up {
  animation: fade-in-up 1s ease-out forwards;
}
</style>