<script setup lang="ts">
import { ref, onErrorCaptured } from 'vue'

const error = ref<string | null>(null)

onErrorCaptured((err) => {
  error.value = err.message
  return false
})
</script>

<template>
  <div v-if="error">
    <h2>Something went wrong</h2>
    <p>{{ error }}</p>
    <button @click="error = null">Try again</button>
  </div>
  <slot v-else />
</template>
