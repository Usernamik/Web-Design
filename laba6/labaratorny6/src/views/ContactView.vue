<script setup lang="ts">
import { reactive, onMounted, watch } from 'vue'
import UserCard from '../components/UserCard.vue'

type Profile = {
  id: number
  username: string
  isActive: boolean
  liked: boolean
  photo?: string | null
}

const state = reactive({
  index: 0,
  profiles: <Profile[]>[
    { id: 1, username: 'Olena', isActive: true, liked: false, photo: null },
    { id: 2, username: 'Andriy', isActive: false, liked: false, photo: null },
    { id: 3, username: 'Nina', isActive: true, liked: false, photo: null }
  ]
})

// Persist profiles to localStorage so added photos and profiles survive reloads
const STORAGE_KEY = 'dating:profiles'

onMounted(() => {
  try {
    const raw = localStorage.getItem(STORAGE_KEY)
    if (raw) {
      const parsed = JSON.parse(raw) as Profile[]
      if (Array.isArray(parsed)) {
        // replace the default profiles with stored ones
        state.profiles.splice(0, state.profiles.length, ...parsed)
      }
    }
  } catch (e) {
    // ignore parse errors
    console.warn('Failed to load profiles from localStorage', e)
  }
})

// Save whenever profiles change
watch(
  () => state.profiles,
  (val) => {
    try {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(val))
    } catch (e) {
      console.warn('Failed to save profiles to localStorage', e)
    }
  },
  { deep: true }
)

function toggleLike(id: number) {
  const p = state.profiles.find((x: Profile) => x.id === id)
  if (p) p.liked = !p.liked
}

function message(id: number) {
  const p = state.profiles.find((x: Profile) => x.id === id)
  if (p) alert(`Start chat with ${p.username}`)
}

function next() {
  // rotate profiles
  const first = state.profiles.shift()
  if (first) state.profiles.push(first)
}

// Form state for creating profile
const form = reactive({ username: '', isActive: false, file: null as File | null })

function onFileChange(e: Event) {
  const input = e.target as HTMLInputElement
  if (!input.files || input.files.length === 0) {
    form.file = null
    return
  }
  form.file = input.files[0]
}

function addProfile() {
  const id = state.profiles.length ? Math.max(...state.profiles.map(p => p.id)) + 1 : 1
  if (!form.username) {
    alert('Please enter username')
    return
  }

  if (form.file) {
    const reader = new FileReader()
    reader.onload = () => {
      state.profiles.push({ id, username: form.username, isActive: form.isActive, liked: false, photo: String(reader.result) })
      form.username = ''
      form.isActive = false
      form.file = null
      const el = document.getElementById('photo-input') as HTMLInputElement | null
      if (el) el.value = ''
    }
    reader.readAsDataURL(form.file)
  } else {
    state.profiles.push({ id, username: form.username, isActive: form.isActive, liked: false, photo: null })
    form.username = ''
    form.isActive = false
  }
}
</script>

<template>
  <div class="p-5">
    <h1 class="text-2xl font-bold mb-4">Dating</h1>
    <p class="mb-4 text-gray-600">Swipe-like demo: like, message, or see next profile.</p>

    <div class="space-y-3">
      <template v-for="p in state.profiles" :key="p.id">
        <UserCard :id="p.id" :username="p.username" :isActive="p.isActive" :liked="p.liked" :photo="p.photo">
          <template #controls>
            <button
              @click.prevent="toggleLike(p.id)"
              :class="p.liked ? 'bg-pink-500 text-white' : 'bg-white border text-pink-500'"
              class="px-3 py-1 rounded-md border shadow-sm"
            >
              {{ p.liked ? 'Liked' : 'Like' }}
            </button>

            <button @click.prevent="message(p.id)" class="px-3 py-1 rounded-md bg-blue-600 text-white">Message</button>

            <button @click.prevent="next" class="px-3 py-1 rounded-md bg-gray-200">Next</button>
          </template>
        </UserCard>
      </template>
    </div>

    <!-- Create profile form -->
    <div class="mt-8 p-4 border-t">
      <h3 class="text-lg font-semibold mb-2">Create your profile</h3>
      <div class="flex flex-col md:flex-row gap-3 md:items-end">
        <div class="flex-1">
          <label class="block text-sm text-gray-700 mb-1">Username</label>
          <input v-model="form.username" class="w-full border rounded px-3 py-2" placeholder="Your name" />
        </div>

        <div>
          <label class="flex items-center gap-2 text-sm">
            <input type="checkbox" v-model="form.isActive" /> <span>Online</span>
          </label>
        </div>

        <div>
          <label class="block text-sm text-gray-700 mb-1">Photo</label>
          <input id="photo-input" type="file" accept="image/*" @change="onFileChange" />
        </div>

        <div>
          <button @click.prevent="addProfile" class="px-4 py-2 bg-green-600 text-white rounded">Add profile</button>
        </div>
      </div>
    </div>
  </div>
</template>
