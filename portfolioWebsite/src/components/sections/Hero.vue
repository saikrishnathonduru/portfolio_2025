<script setup>
import { ref, onMounted } from 'vue';

const startDate = new Date('2021-10-01');
const experience = ref('');
const isVisible = ref(false);

const calculateExperience = () => {
  const now = new Date();
  const diffInMonths = (now.getFullYear() - startDate.getFullYear()) * 12 + 
    (now.getMonth() - startDate.getMonth());
  const years = Math.floor(diffInMonths / 12);
  const months = diffInMonths % 12;
  experience.value = `${years}y ${months}m`;
};

onMounted(() => {
  calculateExperience();
  // Update experience every month
  setInterval(calculateExperience, 30 * 24 * 60 * 60 * 1000);
  // Trigger animation
  setTimeout(() => {
    isVisible.value = true;
  }, 100);
});
</script>

<template>
  <section id="home" class="hero min-h-screen bg-base-100 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 bg-grid-pattern opacity-5"></div>
    <div class="absolute top-20 left-10 w-72 h-72 bg-primary/10 rounded-full filter blur-3xl"></div>
    <div class="absolute bottom-20 right-10 w-72 h-72 bg-secondary/10 rounded-full filter blur-3xl"></div>

    <div class="container mx-auto py-20 px-4 relative">
      <div class="flex flex-col md:flex-row items-center justify-between gap-12">
        <!-- Content Section -->
        <div class="w-full md:w-1/2 text-center md:text-left" :class="{ 'animate-fade-in': isVisible }">
          <!-- Greeting -->
          <div class="inline-block font-mono text-lg mb-4">
            <span class="relative px-4 py-2 text-base-content/70 before:content-[''] before:absolute before:inset-0 before:bg-primary/5 before:rounded-lg before:-skew-x-6">
              Hello, I'm
            </span>
          </div>

          <!-- Name Heading -->
          <h1 class="font-title text-5xl md:text-7xl font-black mb-6 leading-tight">
            <span class="inline-block bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent hover:scale-105 transition-transform cursor-default">
              Saikrishna
            </span>
            <br />
            <span class="inline-block bg-gradient-to-r from-secondary to-primary bg-clip-text text-transparent hover:scale-105 transition-transform cursor-default">
              Thonduru
            </span>
          </h1>

          <!-- Role and Experience -->
          <div class="mb-8 space-y-4">
            <h2 class="text-2xl md:text-3xl font-bold">
              <span class="relative inline-block">
                <span class="relative z-10 text-base-content">Full Stack Data Scientist</span>
                <span class="absolute bottom-0 left-0 w-full h-3 bg-primary/10 -skew-x-6"></span>
              </span>
            </h2>
            <div class="flex items-center justify-center md:justify-start gap-3 text-lg flex-wrap">
              <span class="text-base-content/60">Experience:</span>
              <div class="badge badge-primary badge-lg font-mono shadow-lg shadow-primary/20 animate-pulse">
                {{ experience }}
              </div>
              <span class="text-base-content/60">in AI and Full Stack Development</span>
            </div>
          </div>

          <!-- Social Links -->
          <div class="flex items-center justify-center md:justify-start space-x-4">
            <a 
              href="https://www.linkedin.com/in/saikrishna-thonduru/" 
              target="_blank"
              class="btn btn-circle btn-ghost border border-base-200 hover:border-primary hover:text-primary hover:scale-110 transition-all duration-300 shadow-sm hover:shadow-primary/20"
            >
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
              </svg>
            </a>
            <a 
              href="https://www.xing.com/profile/Saikrishna_Thonduru/web_profiles" 
              target="_blank"
              class="btn btn-circle btn-ghost border border-base-200 hover:border-primary hover:text-primary hover:scale-110 transition-all duration-300 shadow-sm hover:shadow-primary/20"
            >
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path d="M18.188 0c-.517 0-.741.325-.927.66 0 0-7.455 13.224-7.702 13.657.015.024 4.919 9.023 4.919 9.023.17.308.436.66.967.66h3.454c.211 0 .375-.078.463-.22.089-.151.089-.346-.009-.536l-4.879-8.916c-.004-.006-.004-.016 0-.022L22.139.756c.095-.191.097-.387.006-.535C22.056.078 21.894 0 21.686 0h-3.498zM3.648 4.74c-.211 0-.385.074-.473.216-.09.149-.078.339.02.531l2.34 4.05c.004.01.004.016 0 .021L1.86 16.051c-.099.188-.093.381 0 .529.085.142.239.234.45.234h3.461c.518 0 .766-.348.945-.667l3.734-6.609-2.378-4.155c-.172-.315-.434-.659-.962-.659H3.648v.016z"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- Image Section -->
        <div class="w-full md:w-1/2 flex justify-center md:justify-start" :class="{ 'animate-fade-in-delayed': isVisible }">
          <div class="relative w-64 h-64 md:w-96 md:h-96 group">
            <!-- Multiple layered backgrounds for depth -->
            <div class="absolute inset-0 bg-gradient-to-r from-primary to-secondary rounded-2xl rotate-6 opacity-20 group-hover:rotate-12 transition-transform duration-700"></div>
            <div class="absolute inset-0 bg-gradient-to-r from-secondary to-primary rounded-2xl rotate-3 opacity-10 group-hover:rotate-6 transition-transform duration-700"></div>
            <img 
              src="@/assets/cPhoto.jpg" 
              alt="Profile Photo" 
              class="relative z-10 w-full h-full object-cover rounded-2xl shadow-xl transition-transform duration-700 group-hover:scale-105"
            />
            <!-- Decorative elements -->
            <div class="absolute -bottom-4 -right-4 w-24 h-24 bg-primary/10 rounded-full"></div>
            <div class="absolute -top-4 -left-4 w-16 h-16 bg-secondary/10 rounded-full"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.container {
  max-width: 1400px;
}

.bg-grid-pattern {
  background-image: linear-gradient(to right, rgb(var(--primary-rgb) / 0.1) 1px, transparent 1px),
    linear-gradient(to bottom, rgb(var(--primary-rgb) / 0.1) 1px, transparent 1px);
  background-size: 4rem 4rem;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in {
  animation: fadeIn 1s ease-out forwards;
}

.animate-fade-in-delayed {
  animation: fadeIn 1s ease-out 0.3s forwards;
  opacity: 0;
}

/* Ensure image is loaded correctly */
img {
  display: block;
  max-width: 100%;
  height: auto;
}
</style>