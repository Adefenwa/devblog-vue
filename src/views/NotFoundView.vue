<template>
  <div
    class="min-h-screen bg-gray-950 text-gray-100 flex flex-col items-center justify-center px-6"
  >
    <h1 class="text-9xl font-bold text-green-400 mb-4">404</h1>
    <h2 class="text-2xl font-semibold text-white mb-3">Page not found</h2>
    <p class="text-gray-400 mb-8">The page you're looking for doesn't exist.</p>
    <RouterLink
      to="/"
      class="bg-green-400 text-gray-950 px-6 py-3 rounded-lg font-semibold hover:bg-green-300 transition-colors"
    >
      Back to home
    </RouterLink>
  </div>
</template>
