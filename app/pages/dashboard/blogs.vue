<script setup>
import Blogs from "~/components/dashboard/Blogs.vue";

definePageMeta({
  layout: "dashboard",
});
</script>
<template>
  <div>
    <h1 class="text-white">All blog</h1>
    <Blogs />
  </div>
</template>
