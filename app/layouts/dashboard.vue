<script setup>
const route = useRoute();

const isActive = (href) => route.path === href;

const navItems = [
  { name: "Dashboard", href: "/dashboard" },
  { name: "Blogs", href: "/dashboard/blogs" },
  { name: "Users", href: "/dashboard/users" },
  // { name: "Calendar", href: "/calendar" },
];
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <!-- Optional top navbar (import if you have a Navber.vue component) -->
    <Navber />

    <!-- Main Layout -->
    <div class="flex flex-1">
      <!-- Sidebar -->
      <aside class="w-64 bg-gray-700 text-white min-h-screen p-4">
        <nav class="space-y-2">
          <NuxtLink
            v-for="item in navItems"
            :key="item.name"
            :to="item.href"
            :class="[
              isActive(item.href)
                ? 'bg-gray-900 text-white'
                : 'text-gray-300 hover:bg-gray-700 hover:text-white',
              'block px-3 py-2 rounded-md text-sm font-medium',
            ]"
          >
            {{ item.name }}
          </NuxtLink>
        </nav>
      </aside>

      <!-- Page Content -->
      <main class="flex-1 bg-gray-800 p-6">
        <NuxtPage />
      </main>
    </div>
  </div>
</template>
