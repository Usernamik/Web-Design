<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

const isDark = ref(false)

function applyTheme(dark: boolean) {
  const el = document.documentElement
  if (dark) el.classList.add('dark')
  else el.classList.remove('dark')
  isDark.value = dark
  try { localStorage.setItem('theme', dark ? 'dark' : 'light') } catch {}
}

function toggleTheme() {
  applyTheme(!isDark.value)
}

onMounted(() => {
  try {
    const saved = localStorage.getItem('theme')
    if (saved === 'dark') { applyTheme(true); return }
    if (saved === 'light') { applyTheme(false); return }
  } catch {}
  const prefers = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches
  applyTheme(prefers)
})
</script>

<template>
  <header>
    <div class="max-w-4xl mx-auto">
      <nav class="p-4 bg-gray-100 rounded-b-lg shadow-md flex items-center justify-between">

        <div class="flex gap-4 items-center">
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
          <RouterLink to="/contact">Contact</RouterLink>
        </div>

        <div>
          <button
            @click="toggleTheme"
            class="px-3 py-1 border rounded bg-white hover:bg-gray-50 text-sm dark:bg-gray-700 dark:text-white"
            aria-label="Toggle theme"
          >
            {{ isDark ? 'Light' : 'Dark' }} Mode
          </button>
        </div>

      </nav>
    </div>
  </header>

  <main class="max-w-4xl mx-auto mt-5">
    <RouterView />
  </main>
</template>
