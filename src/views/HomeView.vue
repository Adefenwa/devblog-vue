<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

interface Post {
  id: string
  title: string
  excerpt: string | null
  content: string
  slug: string | null
  category: string | null
  viewCount: number
  author: string | null
  createdAt: string
}

const router = useRouter()
const posts = ref<Post[]>([])
const loading = ref(true)
const error = ref<string | null>(null)

onMounted(async () => {
  try {
    const res = await fetch('https://api.oluwasetemi.dev/posts')
    const json = await res.json()
    posts.value = json.data
  } catch {
    error.value = 'Failed to load posts'
  } finally {
    loading.value = false
  }
})

function goToPost(id: string) {
  router.push({ name: 'post-detail', params: { id } })
}
</script>

<template>
  <div class="min-h-screen bg-gray-950 text-gray-100">
    <div class="max-w-3xl mx-auto px-6 py-16">
      <div class="mb-12">
        <h1 class="text-5xl font-bold text-white mb-3">DevBlogg 2.0</h1>
        <p class="text-gray-400">Stories, ideas and things worth reading.</p>
      </div>

      <p v-if="loading" class="text-gray-400 animate-pulse">Loading posts...</p>
      <p v-else-if="error" class="text-red-400">{{ error }}</p>

      <ul
        v-else
        class="flex flex-col gap-px bg-gray-800 border border-gray-800 rounded-xl overflow-hidden"
      >
        <li
          v-for="post in posts"
          :key="post.id"
          @click="goToPost(post.id)"
          class="bg-gray-900 px-6 py-5 cursor-pointer hover:bg-gray-800 transition-colors group"
        >
          <h2
            class="text-lg font-semibold text-white group-hover:text-green-400 transition-colors mb-1"
          >
            {{ post.title }}
          </h2>
          <p class="text-gray-400 text-sm line-clamp-2">{{ post.excerpt ?? post.content }}</p>
        </li>
      </ul>
    </div>
    <footer>
      <div class="max-w-3xl mx-auto px-6 py-8 text-center text-gray-500 text-sm">
        &copy; 2026 DevBlogg. All rights reserved. Built with Vue by Adefenwa
      </div>
    </footer>
  </div>
</template>
