<script setup>
// Example static blog post data
const posts = [
  {
    id: 1,
    title: "Getting Started with Nuxt 4",
    summary: "Learn how to create your first Nuxt 4 app.",
    slug: "getting-started-nuxt-4",
  },
  {
    id: 2,
    title: "Tailwind CSS in Nuxt",
    summary: "A quick guide to using Tailwind CSS in Nuxt projects.",
    slug: "tailwind-in-nuxt",
  },
  {
    id: 3,
    title: "Deploying Nuxt with Vercel",
    summary: "Steps to deploy your Nuxt 4 app on Vercel.",
    slug: "deploying-nuxt-vercel",
  },
  {
    id: 4,
    title: "Using Composables in Nuxt",
    summary: "How to organize logic using Vue composables in Nuxt.",
    slug: "using-composables-nuxt",
  },
];
</script>

<template>
  <div class="py-12 bg-gray-900 min-h-screen">
    <div class="max-w-5xl mx-auto px-4">
      <h1 class="text-3xl text-white font-bold mb-8">📚 Blog Posts</h1>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
        <NuxtLink
          v-for="post in posts"
          :key="post.id"
          :to="`/blog/${post.slug}`"
          class="block bg-gray-800 border border-gray-700 rounded-lg p-6 hover:shadow-lg hover:border-gray-500 transition"
        >
          <h2 class="text-xl font-semibold text-white mb-2 hover:underline">
            {{ post.title }}
          </h2>
          <p class="text-gray-400 text-sm">{{ post.summary }}</p>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
