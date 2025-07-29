<script setup>
import { useRoute } from "vue-router";

const route = useRoute();

const blogPosts = {
  "getting-started-nuxt-4": {
    title: "Getting Started with Nuxt 4",
    content: "This is the full content of the Nuxt 4 getting started post.",
  },
  "tailwind-in-nuxt": {
    title: "Tailwind CSS in Nuxt",
    content: "Tailwind makes styling in Nuxt super easy.",
  },
};

const post = blogPosts[route.params.slug];
</script>

<template>
  <div class="bg-gray-900 min-h-screen py-10">
    <div class="max-w-4xl mx-auto px-4">
      <div v-if="post">
        <h1 class="text-3xl font-bold text-white mb-4">{{ post.title }}</h1>
        <p class="text-gray-300 leading-relaxed">{{ post.content }}</p>
      </div>

      <!-- 404 Centered -->
      <div
        v-else
        class="flex flex-col items-center justify-center text-center h-[60vh]"
      >
        <h2 class="text-2xl font-bold text-red-400 mb-2">
          404 - Post not found
        </h2>
        <p class="text-gray-400 mb-4">
          Sorry, the blog post you're looking for does not exist.
        </p>
        <NuxtLink to="/blog" class="inline-block text-blue-400 hover:underline">
          ← Back to Blog
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
