<!-- Navigation.vue -->
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { AkHomeAlt1 } from '@kalimahapps/vue-icons';

const activeSection = ref('home')
const isScrolled = ref(false)

const navItems = [
  { id: 'home', label: 'Home', icon: '🏠' },
  { id: 'about', label: 'About', icon: '👤' },
  { id: 'projects', label: 'Projects', icon: '💼' },
  //{ id: 'experience', label: 'Experience', icon: '📈' },
  { id: 'testimonial', label: 'Testimonial', icon: '💬' }
//   { id: 'contact', label: 'Contact', icon: '📧' }
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

const observeSection = () => {
  const sections = document.querySelectorAll('section[id]')
  const navLinks = document.querySelectorAll('.nav-link')
  
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        activeSection.value = entry.target.id
      }
    })
  }, { threshold: 0.5 })
  
  sections.forEach(section => {
    observer.observe(section)
  })
  
  // Clean up on component unmount
  onUnmounted(() => {
    sections.forEach(section => {
      observer.unobserve(section)
    })
  })
}

const handleNavClick = (id) => {
  const element = document.getElementById(id)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  observeSection()
  window.addEventListener('scroll', handleScroll)
})
</script>

<template>
  <div class="fixed top-0 left-0 right-0 z-50 p-4" :class="{ 'backdrop-blur-sm': isScrolled }">
    <nav class="container mx-auto bg-base-100/80 backdrop-blur-sm rounded-full border border-base-200 shadow-lg transition-all duration-300"
         :class="{ 'shadow-primary/5': isScrolled }">
      <div class="flex items-center justify-between h-16 px-6">
        <!-- Logo -->
        <a href="#home" class="text-xl font-bold bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent hover:opacity-80 transition-all duration-300">
          Portfolio
        </a>

        <!-- Navigation Links -->
        <div class="hidden md:flex items-center space-x-8">
          <a v-for="item in navItems"
             :key="item.id"
             :href="`#${item.id}`"
             @click="handleNavClick(item.id)"
             class="nav-link relative px-2 py-2 text-base-content/70 hover:text-primary transition-all duration-300"
             :class="{ 'text-primary font-medium': activeSection === item.id }">
            <span class="mr-2">{{ item.icon }}</span>
            {{ item.label }}
          </a>
        </div>

        <!-- Get in Touch Button -->
        <a href="#contact" 
           class="hidden md:block px-6 py-2 rounded-full bg-gradient-to-r from-primary to-secondary text-primary-content hover:shadow-lg hover:shadow-primary/20 transition-all duration-300 transform hover:scale-105">
          Get in Touch
        </a>

        <!-- Mobile Menu Button -->
        <button class="md:hidden btn btn-ghost btn-circle text-base-content/70 hover:bg-base-200/50">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h7" />
          </svg>
        </button>
      </div>
    </nav>
  </div>
</template>

<style scoped>
.container {
  max-width: 1400px;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 2px;
  background: linear-gradient(to right, theme('colors.primary'), theme('colors.secondary'));
  transition: all 0.3s ease;
  transform: translateX(-50%);
  opacity: 0;
}

.nav-link:hover::after {
  width: 100%;
  opacity: 1;
}

nav {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.03);
}
</style>