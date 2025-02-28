<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  variant?: 'default' | 'primary' | 'secondary' | 'outline' | 'ghost'
  size?: 'sm' | 'md' | 'lg'
  type?: 'button' | 'submit' | 'reset'
}>()

const classes = computed(() => {
  return {
    'btn': true,
    [`btn-${props.variant || 'default'}`]: true,
    [`btn-${props.size || 'md'}`]: true,
  }
})
</script>

<template>
  <button :type="type" :class="classes">
    <slot></slot>
  </button>
</template>

<style scoped>
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 0.375rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-default {
  background-color: #fff;
  border: 1px solid #e2e8f0;
  color: #1a202c;
}

.btn-primary {
  background-color: #3182ce;
  color: white;
  border: none;
}

.btn-secondary {
  background-color: #718096;
  color: white;
  border: none;
}

.btn-outline {
  background-color: transparent;
  border: 1px solid #3182ce;
  color: #3182ce;
}

.btn-ghost {
  background-color: transparent;
  border: none;
  color: #3182ce;
}

.btn-sm {
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
}

.btn-md {
  padding: 0.625rem 1.25rem;
  font-size: 1rem;
}

.btn-lg {
  padding: 0.75rem 1.5rem;
  font-size: 1.125rem;
}
</style>