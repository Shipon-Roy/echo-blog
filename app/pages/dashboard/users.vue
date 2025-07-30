<script setup>
import Error from "~/components/Error.vue";
import Loader from "~/components/Loader.vue";

definePageMeta({
  layout: "dashboard",
});

// Fetch blog data
const {
  data: users,
  error,
  pending,
} = await useFetch("https://fakestoreapi.com/users");
</script>

<template>
  <div>
    <Error v-if="error" title="Blog Not Found." />
    <Loader v-else-if="pending" />

    <div v-if="users" class="relative overflow-x-auto mt-10">
      <table
        class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
      >
        <thead
          class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
        >
          <tr>
            <th scope="col" class="px-6 py-3">Name</th>
            <th scope="col" class="px-6 py-3">Email</th>
            <th scope="col" class="px-6 py-3">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(user, index) in users"
            :key="index"
            class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 border-gray-200"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ user.username }}
            </th>
            <td class="px-6 py-4">{{ user.email }}</td>
            <td class="px-6 py-4 flex items-center gap-4">
              <!-- Edit Icon -->
              <span class="text-blue-500 cursor-pointer"> ✎ </span>
              <!-- Delete Icon -->
              <span class="text-red-500 cursor-pointer"> 🗑 </span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
