<script setup>
import { ref } from "vue";
import Error from "../Error.vue";
import Loader from "../Loader.vue";
import Modal from "../Modal.vue";

definePageMeta({
  layout: "dashboard",
});

// Fetch blog data
const {
  data: blogs,
  error,
  pending,
} = await useFetch("https://fakestoreapi.com/products");

// Modal control
const showModal = ref(false);

// Form fields
const title = ref("");
const description = ref("");
const price = ref("");

// Add blog handler
const handleSubmit = () => {
  if (!title.value || !description.value || !price.value) return;

  blogs.value.push({
    title: title.value,
    description: description.value,
    price: parseFloat(price.value),
  });

  title.value = "";
  description.value = "";
  price.value = "";
  showModal.value = false;
};
</script>

<template>
  <div>
    <Error v-if="error" title="Blog Not Found." />
    <Loader v-else-if="pending" />

    <div v-if="blogs" class="relative overflow-x-auto mt-10">
      <div class="flex justify-end m-5">
        <button
          class="bg-gray-700 text-white py-2 px-4 rounded"
          @click="showModal = true"
        >
          Add New
        </button>
      </div>

      <table
        class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
      >
        <thead
          class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
        >
          <tr>
            <th scope="col" class="px-6 py-3">Product name</th>
            <th scope="col" class="px-6 py-3">Price</th>
            <th scope="col" class="px-6 py-3">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(blog, index) in blogs"
            :key="index"
            class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 border-gray-200"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ blog.title }}
            </th>
            <td class="px-6 py-4">{{ blog.price }}</td>
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

    <!-- Modal -->
    <Modal v-if="showModal" @close="showModal = false">
      <h2 class="text-xl text-white font-bold mb-4">Add New Blog</h2>
      <form @submit.prevent="handleSubmit" class="flex flex-col space-y-4">
        <input
          v-model="title"
          type="text"
          placeholder="Title"
          class="border border-white text-gray-100 p-2 rounded"
          required
        />
        <textarea
          v-model="description"
          placeholder="Description"
          class="border border-white text-gray-100 p-2 rounded"
          required
        ></textarea>
        <input
          v-model="price"
          type="number"
          placeholder="Price"
          class="border border-white text-gray-100 p-2 rounded"
          required
        />
        <div class="flex justify-end gap-4">
          <button
            type="button"
            class="text-gray-100"
            @click="showModal = false"
          >
            Cancel
          </button>
          <button
            type="submit"
            class="bg-blue-600 text-white px-4 py-2 rounded"
          >
            Save
          </button>
        </div>
      </form>
    </Modal>
  </div>
</template>
