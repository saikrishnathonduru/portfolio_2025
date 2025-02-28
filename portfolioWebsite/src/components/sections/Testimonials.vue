<template>
  <section id="testimonial" class="py-24 scroll-mt-24 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 bg-gradient-to-br from-white via-purple-50/30 to-white"></div>
    <div class="absolute top-0 left-0 w-full h-full bg-grid-pattern opacity-5"></div>
    <div class="absolute top-20 -left-32 w-80 h-80 bg-primary/10 rounded-full filter blur-3xl animate-pulse"></div>
    <div class="absolute bottom-20 -right-32 w-80 h-80 bg-secondary/10 rounded-full filter blur-3xl animate-pulse" style="animation-delay: 2s;"></div>

    <div class="container mx-auto px-4 relative">
      <!-- Section Header -->
      <div class="text-center mb-8">
        <h2 class="text-3xl font-bold mb-2 bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent animate-fade-in-up">
          Testimonials
        </h2>
        <div class="w-16 h-1 bg-gradient-to-r from-primary to-secondary mx-auto rounded-full"></div>
      </div>

      <!-- Testimonials Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div v-for="(testimonial, index) in testimonials" 
             :key="index"
             class="group">
          <div class="bg-white/40 backdrop-blur-lg rounded-xl p-4 shadow-md border border-white/20 
                    hover:shadow-lg transition-all duration-500 h-full relative overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-br from-primary/5 to-transparent opacity-0 
                      group-hover:opacity-100 transition-opacity duration-500"></div>
            
            <!-- Quote Icon -->
            <div class="text-primary/20 text-3xl mb-2">"</div>
            
            <!-- Testimonial Content -->
            <p class="text-gray-700 text-sm mb-4 relative">{{ testimonial.content }}</p>
            
            <!-- Author Info -->
            <div class="flex items-center space-x-3 relative">
              <div class="w-10 h-10 rounded-full bg-gradient-to-r from-primary to-secondary flex items-center justify-center text-white text-xs font-bold">
                {{ getInitials(testimonial.name) }}
              </div>
              <div>
                <h4 class="font-semibold text-gray-800 text-sm">{{ testimonial.name }}</h4>
                <p class="text-xs text-gray-600">{{ testimonial.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const testimonials = [
  {
    content: "I highly recommend Saikrishna Thonduru, an outstanding AI Data Scientist who has transformed our AI capabilities and business intelligence. He has developed Power BI dashboards, AI-powered platforms, and advanced chatbots using Retrieval-Augmented Generation (RAG). His expertise in term extraction, SEO optimization, and speech-to-text services, combined with his strategic thinking and problem-solving skills, makes him a valuable asset to any team.",
    name: "David Benotmane",
    role: "Tech Strategist at Kern AG"
  },
  {
    content: "An outstanding professional who consistently delivers high-quality work. Their deep understanding of ML systems and attention to detail resulted in significant improvements to our data processing pipeline.",
    name: "Maren Zieger",
    role: "Head of Systems Engineering at KERN AG"
  },
  {
    content: "Exceptional problem-solving skills and technical expertise. They brought valuable insights to our AI implementation and helped us achieve our project goals ahead of schedule.",
    name: "Thomas Kern",
    role: "CTO at KERN AG"
  }
];

// Function to get first and last letter of a name
const getInitials = (name) => {
  if (!name) return '';
  const nameParts = name.split(' ');
  if (nameParts.length === 1) {
    // If only one name, return first and last letter of that name
    const singleName = nameParts[0];
    return singleName.charAt(0) + singleName.charAt(singleName.length - 1);
  }
  // Get first letter of first name and first letter of last name
  const firstName = nameParts[0];
  const lastName = nameParts[nameParts.length - 1];
  return firstName.charAt(0) + lastName.charAt(0);
};
</script>

<style scoped>
.bg-grid-pattern {
  background-image: linear-gradient(to right, rgba(0,0,0,0.1) 1px, transparent 1px),
                    linear-gradient(to bottom, rgba(0,0,0,0.1) 1px, transparent 1px);
  background-size: 20px 20px;
}
</style>