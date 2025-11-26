<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  id: number
  username: string
  isActive: boolean
  liked?: boolean
  photo?: string | null
}>()

const statusText = computed(() => (props.isActive ? 'Онлайн' : 'Офлайн'))
</script>

<template>
  <div 
    class="border p-4 mt-3 rounded-lg shadow-sm flex items-center justify-between"
    :class="props.isActive 
      ? 'border-green-500 bg-green-50 dark:bg-green-900 dark:border-green-700' 
      : 'border-gray-300 bg-white dark:bg-gray-800 dark:border-gray-600'"
  >
    <div>
        <div class="flex items-center gap-3">
          <img v-if="props.photo" :src="props.photo" alt="avatar" class="w-12 h-12 rounded-full object-cover border" />
          <div>
            <h3 class="font-semibold text-lg dark:text-white">{{ props.username }}</h3>
            <p class="text-sm" :class="props.isActive ? 'text-green-700' : 'text-gray-500'">Статус: {{ statusText }}</p>
          </div>
        </div>
    </div>

    <div class="flex items-center gap-2">
      <slot name="controls" />
    </div>
  </div>
</template>
