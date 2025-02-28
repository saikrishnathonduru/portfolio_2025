<template>
  <div class="min-h-screen bg-base-100">
    <!-- Navigation -->
    <Navigation />

    <!-- Main Content -->
    <main class="container mx-auto px-4">
      <!-- Hero Section -->
      <Hero />

      <!-- Other Sections -->
      <About />
      
      <Projects />
      <Testimonials />
      <Contact />
    </main>

    <!-- Footer -->
    <footer class="footer footer-center p-4 bg-base-200 text-base-content">
      <div>
        <p>© {{ new Date().getFullYear() }} Saikrishna Thonduru. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { defineAsyncComponent, ref, onMounted } from 'vue'

// Lazy load components that aren't immediately visible
const Skills = defineAsyncComponent(() => import('./components/sections/Skills.vue'))
const Projects = defineAsyncComponent(() => import('./components/sections/Projects.vue'))
const Contact = defineAsyncComponent(() => import('./components/sections/Contact.vue'))
//const Experience = defineAsyncComponent(() => import('./components/sections/Experience.vue'))
const Testimonials = defineAsyncComponent(() => import('./components/sections/Testimonials.vue'))

// Keep immediate components loaded normally
import Hero from './components/sections/Hero.vue'
import Navigation from './components/Navigation.vue'
import About from './components/sections/About.vue'

const sections = [
  { id: 'home', label: 'Home' },
  { id: 'about', label: 'About' },
  { id: 'skills', label: 'Skills' },
  //{ id: 'experience', label: 'Experience' },
  { id: 'projects', label: 'Projects' },
  { id: 'testimonial', label: 'Testimonial' },
  { id: 'contact', label: 'Contact' }
]

const activeSection = ref('about')
const isMenuOpen = ref(false)
const hasScrolled = ref(false)

const stats = [
  { label: 'Years Experience', value: '3+', icon: '' },
  { label: 'Projects Completed', value: '20+', icon: '' },
  { label: 'Technologies', value: '15+', icon: '' }
]

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  initializeParallax()
})

const handleScroll = () => {
  hasScrolled.value = window.scrollY > 50
}

const initializeParallax = () => {
  const parallaxElements = document.querySelectorAll('.parallax')
  window.addEventListener('scroll', () => {
    parallaxElements.forEach(el => {
      const speed = el.dataset.speed || 0.5
      const yPos = -(window.scrollY * speed)
      el.style.transform = `translateY(${yPos}px)`
    })
  })
}
</script>

<style>


.container {
  width: 100%;
  max-width: 1400px;
}
</style>