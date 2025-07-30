<template>
  <div
    class="fixed inset-0 bg-gray-800 bg-opacity-50 flex justify-center items-center z-50"
  >
    <div class="bg-gray-700 p-6 rounded-md w-full max-w-2xl shadow-md relative">
      <button
        @click="$emit('close')"
        class="absolute top-2 right-2 text-gray-100 text-xl"
      >
        ✕
      </button>
      <slot />
    </div>
  </div>
</template>
