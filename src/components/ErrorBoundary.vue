<script setup lang="ts">
import { ref, onErrorCaptured } from 'vue'

const error = ref<string | null>(null)

onErrorCaptured((err) => {
  error.value = err.message
  return false
})
</script>

<template>
  <div v-if="error" class="min-h-screen bg-gray-950 flex flex-col items-center justify-center px-6">
    <div class="bg-gray-900 border border-red-800 rounded-xl p-8 max-w-md w-full text-center">
      <h2 class="text-xl font-bold text-red-400 mb-2">Something went wrong</h2>
      <p class="text-gray-400 text-sm mb-6">{{ error }}</p>
      <button
        @click="error = null"
        class="bg-red-500 text-white px-5 py-2 rounded-lg text-sm hover:bg-red-400 transition-colors"
      >
        Try again
      </button>
    </div>
  </div>
  <slot v-else />
</template>
