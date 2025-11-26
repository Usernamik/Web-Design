<script setup lang="ts">
</script>

<template>
  <section class="p-6">
    <div class="max-w-5xl mx-auto bg-white dark:bg-gray-900 rounded-2xl shadow-lg overflow-hidden">
      <div class="md:flex">
        <!-- Left: Illustration / Photo -->
        <div class="md:w-1/2 bg-gradient-to-br from-pink-50 to-white dark:from-pink-900 dark:to-gray-800 p-6 flex items-center justify-center">
          <!-- Hero SVG image (local asset) -->
          <img src="@/assets/hero-2.svg" alt="Dating hero" class="w-64 h-64 object-cover rounded-xl shadow-md ring-4 ring-white/70 dark:ring-black/40" />
        </div>

        <!-- Right: Text -->
        <div class="md:w-1/2 p-8 flex flex-col justify-center">
          <h1 class="text-4xl font-extrabold text-gray-900 dark:text-white mb-4">Dating</h1>

          <div class="flex gap-3">
            <router-link to="/meet" class="inline-block px-5 py-3 bg-pink-500 text-white rounded-lg shadow hover:bg-pink-600">Start</router-link>
            <router-link to="/about" class="inline-block px-5 py-3 border border-gray-200 rounded-lg text-gray-700 hover:bg-gray-50 dark:text-gray-200">About</router-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
