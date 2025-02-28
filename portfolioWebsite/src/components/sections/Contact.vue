<template>
  <section id="contact" class="py-24 relative overflow-hidden">
    <!-- Background Elements -->
    <div class="absolute inset-0 bg-grid-pattern opacity-5"></div>
    <div class="absolute top-20 left-10 w-64 h-64 bg-primary/10 rounded-full filter blur-3xl"></div>
    <div class="absolute bottom-20 right-10 w-64 h-64 bg-secondary/10 rounded-full filter blur-3xl"></div>

    <div class="container mx-auto px-4 relative">
      <!-- Section Header -->
      <div class="text-center max-w-2xl mx-auto mb-8">
        <h2 class="text-3xl font-bold mb-3 bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent">
          Get in Touch
        </h2>
        <p class="text-base-content/60 text-base">
          Feel free to reach out for collaboration opportunities, questions about my work, 
          or just to say hello. I'm always open to discussing new projects and ideas.
        </p>
      </div>

      <!-- Contact Form -->
      <div class="max-w-xl mx-auto">
        <div class="bg-base-100/50 backdrop-blur-sm p-6 rounded-xl shadow-md border border-base-200">
          <!-- Success Message -->
          <div v-if="submitStatus === 'success'" class="alert alert-success mb-4 text-sm">
            <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-5 w-5" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
            <span>Thank you! Your message has been sent successfully.</span>
          </div>
          
          <!-- Error Message -->
          <div v-if="submitStatus === 'error'" class="alert alert-error mb-4 text-sm">
            <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-5 w-5" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
            <span>{{ errorMessage || 'Failed to submit the form. Please try again later.' }}</span>
          </div>
          
          <!-- Google Apps Script Form -->
          <form 
            v-if="submitStatus !== 'success'"
            ref="contactForm" 
            :action="scriptUrl" 
            method="POST" 
            target="hidden-iframe" 
            @submit="handleFormSubmit"
            class="space-y-4"
          >
            <!-- Name Input -->
            <div class="form-control">
              <label class="label">
                <span class="label-text text-sm font-medium">Name</span>
              </label>
              <input 
                type="text" 
                name="name"
                v-model="formData.name"
                class="input input-bordered w-full focus:input-primary transition-all duration-300 text-sm"
                placeholder="Your name"
                required
              />
            </div>

            <!-- Email Input -->
            <div class="form-control">
              <label class="label">
                <span class="label-text text-sm font-medium">Email</span>
              </label>
              <input 
                type="email" 
                name="email"
                v-model="formData.email"
                class="input input-bordered w-full focus:input-primary transition-all duration-300 text-sm"
                placeholder="your.email@example.com"
                required
              />
            </div>

            <!-- Message Input -->
            <div class="form-control">
              <label class="label">
                <span class="label-text text-sm font-medium">Message</span>
              </label>
              <textarea 
                name="message"
                v-model="formData.message"
                class="textarea textarea-bordered h-28 focus:textarea-primary transition-all duration-300 text-sm"
                placeholder="Your message here..."
                required
              ></textarea>
            </div>

            <!-- Submit Button -->
            <button 
              type="submit"
              class="btn btn-primary w-full bg-gradient-to-r from-primary to-secondary hover:shadow-lg hover:shadow-primary/20 border-0 transition-all duration-300 text-sm"
              :disabled="isSubmitting"
            >
              <span v-if="isSubmitting">
                <span class="loading loading-spinner loading-sm mr-2"></span>
                Sending...
              </span>
              <span v-else>Send Message</span>
            </button>
          </form>
          
          <!-- Hidden iframe for form submission -->
          <iframe 
            name="hidden-iframe" 
            ref="hiddenIframe"
            style="display:none" 
            @load="handleIframeLoad"
          ></iframe>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, ref, onMounted } from 'vue'

const formData = reactive({
  name: '',
  email: '',
  message: ''
})

const isSubmitting = ref(false)
const submitStatus = ref(null) // null, 'success', 'error'
const errorMessage = ref('')
const hiddenIframe = ref(null)

// Google Apps Script web app URL
const scriptUrl = 'https://script.google.com/macros/s/AKfycbzmLeXSdO_rgXOE_mK9ulAj9_RTzG8DAdZx70O_YAkelAfNRp6aQjuS1aouDL-VgXJ5/exec'

// Handle form submission
const handleFormSubmit = async (e) => {
  e.preventDefault()
  isSubmitting.value = true
  submitStatus.value = null
  
  try {
    // Use fetch API for better control and error handling
    await fetch(scriptUrl, {
      method: 'POST',
      mode: 'no-cors', // Important for cross-origin requests to Google Forms
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body: new URLSearchParams({
        name: formData.name,
        email: formData.email,
        message: formData.message
      })
    })
    
    // With no-cors mode, we can't read the response
    // So we'll assume success if no error is thrown
    
    // Success case
    submitStatus.value = 'success'
    // Clear the form
    formData.name = ''
    formData.email = ''
    formData.message = ''
    // Auto-dismiss success message after 5 seconds
    setTimeout(() => {
      submitStatus.value = null
    }, 5000)
  } catch (error) {
    console.error('Form submission error:', error)
    submitStatus.value = 'error'
    errorMessage.value = 'Something went wrong. Please try again.'
    // Auto-dismiss error message after 5 seconds
    setTimeout(() => {
      submitStatus.value = null
      errorMessage.value = ''
    }, 5000)
  } finally {
    isSubmitting.value = false
  }
}

// Handle iframe load event (alternative approach if fetch doesn't work)
const handleIframeLoad = (event) => {
  // Only process if we're submitting
  if (!isSubmitting.value) return
  
  try {
    const iframeContent = hiddenIframe.value.contentDocument || hiddenIframe.value.contentWindow.document
    const responseText = iframeContent.body.innerText || iframeContent.body.textContent
    
    // Try to parse the response as JSON
    let response
    try {
      response = JSON.parse(responseText)
    } catch (e) {
      // If not valid JSON, check if it contains success message
      if (responseText.includes('success')) {
        response = { success: true }
      } else {
        response = { success: false, error: responseText }
      }
    }
    
    if (response.success) {
      submitStatus.value = 'success'
      // Clear the form
      formData.name = ''
      formData.email = ''
      formData.message = ''
      // Auto-dismiss success message after 5 seconds
      setTimeout(() => {
        submitStatus.value = null
      }, 5000)
    } else {
      submitStatus.value = 'error'
      errorMessage.value = response.error || 'Failed to submit the form. Please try again later.'
      // Auto-dismiss error message after 5 seconds
      setTimeout(() => {
        submitStatus.value = null
        errorMessage.value = ''
      }, 5000)
    }
  } catch (error) {
    console.error('Error processing iframe response:', error)
    submitStatus.value = 'error'
    errorMessage.value = 'Something went wrong. Please try again.'
    // Auto-dismiss error message after 5 seconds
    setTimeout(() => {
      submitStatus.value = null
      errorMessage.value = ''
    }, 5000)
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
.container {
  max-width: 1400px;
}

.bg-grid-pattern {
  background-image: linear-gradient(to right, rgb(var(--primary-rgb) / 0.1) 1px, transparent 1px),
    linear-gradient(to bottom, rgb(var(--primary-rgb) / 0.1) 1px, transparent 1px);
  background-size: 4rem 4rem;
}

/* Custom focus styles */
.input:focus, .textarea:focus {
  outline: none;
  border-color: theme('colors.primary');
  box-shadow: 0 0 0 1px theme('colors.primary');
}
</style>