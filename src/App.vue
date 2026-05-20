<script setup lang="ts">
import { RouterView } from 'vue-router'
import { defineAsyncComponent } from 'vue'

const ErrorBoundary = defineAsyncComponent(() => import('./components/ErrorBoundary.vue'))
</script>

<template>
  <ErrorBoundary>
    <RouterView v-slot="{ Component }">
      <Suspense>
        <template #default>
          <component :is="Component" />
        </template>
        <template #fallback>
          <p>Loading page...</p>
        </template>
      </Suspense>
    </RouterView>
  </ErrorBoundary>
</template>
