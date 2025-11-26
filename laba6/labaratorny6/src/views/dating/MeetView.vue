<script setup lang="ts">
</script>

<template>
  <section class="min-h-screen flex items-center justify-center bg-gray-50 dark:bg-gray-900 p-8">
    <div class="max-w-3xl w-full bg-white dark:bg-gray-800 rounded-xl shadow-lg overflow-hidden p-6 text-center">
      <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">This site was be create for meeting you love</h2>

      <div class="flex items-center justify-center">
        <img src="../../assets/hero-2.png" alt="Couple" class="w-full max-w-xl object-contain rounded-lg shadow" />
      </div>

      <p class="mt-6 text-gray-600 dark:text-gray-300">Find new connections — like, message and meet people who share your interests.</p>

      <div class="mt-6 flex justify-center">
        <router-link to="/contact" class="px-6 py-3 bg-pink-500 text-white rounded-lg shadow hover:bg-pink-600">Go dating</router-link>
      </div>
    </div>
  </section>
</template>
