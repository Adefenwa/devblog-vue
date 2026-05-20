<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

interface Post {
  id: string
  title: string
  content: string
  excerpt: string | null
  author: string | null
  category: string | null
  createdAt: string
}

const route = useRoute()
const router = useRouter()
const post = ref<Post | null>(null)
const loading = ref(true)
const error = ref<string | null>(null)

onMounted(async () => {
  try {
    const res = await fetch(`https://api.oluwasetemi.dev/posts/${route.params.id}`)
    if (!res.ok) throw new Error('Post not found')
    post.value = await res.json()
  } catch {
    error.value = 'Failed to load post'
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <div class="min-h-screen bg-gray-950 text-gray-100">
    <div class="max-w-3xl mx-auto px-6 py-16">
      <button
        @click="router.back()"
        class="flex items-center gap-2 text-gray-400 cursor-pointer hover:text-white transition-colors mb-12 text-sm"
      >
        ← Back
      </button>

      <p v-if="loading" class="text-gray-400 animate-pulse">Loading post...</p>
      <p v-else-if="error" class="text-red-400">{{ error }}</p>

      <article v-else-if="post">
        <div class="mb-2 flex items-center gap-3 text-sm text-gray-500">
          <span>{{ post.author ?? 'Unknown' }}</span>
          <span>·</span>
          <span>{{ post.category ?? 'General' }}</span>
          <span>·</span>
          <span>{{ new Date(post.createdAt).toLocaleDateString() }}</span>
        </div>

        <h1 class="text-4xl font-bold text-white mb-8 leading-tight">{{ post.title }}</h1>

        <div class="w-12 h-1 bg-green-400 mb-8 rounded-full"></div>

        <p class="text-gray-300 leading-relaxed text-lg">{{ post.content }}</p>
      </article>
    </div>
  </div>
</template>
