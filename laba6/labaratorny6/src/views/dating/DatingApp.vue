<template>
  <div class="max-w-2xl mx-auto bg-white p-6 rounded-lg shadow">
    <h1 class="text-2xl font-semibold mb-4">Dating App — Create Profile</h1>

    <form @submit.prevent="onSubmit" class="space-y-4">
      <div>
        <label class="block text-sm font-medium text-gray-700">Name</label>
        <input v-model="form.name" type="text" class="mt-1 block w-full rounded border px-3 py-2" />
        <p v-if="errors.name" class="text-sm text-red-600 mt-1">{{ errors.name }}</p>
      </div>

      <div>
        <label class="block text-sm font-medium text-gray-700">Email</label>
        <input v-model="form.email" type="email" class="mt-1 block w-full rounded border px-3 py-2" />
        <p v-if="errors.email" class="text-sm text-red-600 mt-1">{{ errors.email }}</p>
      </div>

      <div>
        <label class="block text-sm font-medium text-gray-700">Age</label>
        <input v-model.number="form.age" type="number" min="0" class="mt-1 block w-32 rounded border px-3 py-2" />
        <p v-if="errors.age" class="text-sm text-red-600 mt-1">{{ errors.age }}</p>
      </div>

      <div>
        <label class="block text-sm font-medium text-gray-700">Photo (optional)</label>
        <input @change="onFileChange" type="file" accept="image/*" class="mt-1 block" />
        <img v-if="preview" :src="preview" alt="preview" class="mt-2 w-32 h-32 object-cover rounded-full" />
      </div>

      <div class="flex items-center gap-3">
        <label class="inline-flex items-center">
          <input type="checkbox" v-model="saveToProfiles" class="mr-2" />
          <span class="text-sm text-gray-700">Save to local profiles</span>
        </label>
      </div>

      <div class="flex items-center gap-3">
        <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded">Submit</button>
        <button type="button" @click="resetForm" class="text-gray-700 px-3 py-2 rounded border">Reset</button>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'

type Form = {
  name: string
  email: string
  age: number | null
  photo?: string | null
}

const form = reactive<Form>({ name: '', email: '', age: null, photo: null })
const errors = reactive<{ [k: string]: string | null }>({ name: null, email: null, age: null })
const preview = ref<string | null>(null)
const saveToProfiles = ref(false)

function validate() {
  let ok = true
  errors.name = null
  errors.email = null
  errors.age = null

  if (!form.name || !form.name.trim()) {
    errors.name = 'Name is required.'
    ok = false
  }

  const emailRe = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!form.email || !emailRe.test(form.email)) {
    errors.email = 'Please enter a valid email address.'
    ok = false
  }

  if (form.age == null || Number.isNaN(form.age)) {
    errors.age = 'Age is required.'
    ok = false
  } else if (form.age < 18) {
    errors.age = 'You must be at least 18.'
    ok = false
  }

  return ok
}

function onFileChange(e: Event) {
  const input = e.target as HTMLInputElement
  const file = input.files && input.files[0]
  if (!file) return
  const reader = new FileReader()
  reader.onload = () => {
    form.photo = String(reader.result || null)
    preview.value = form.photo
  }
  reader.readAsDataURL(file)
}

function resetForm() {
  form.name = ''
  form.email = ''
  form.age = null
  form.photo = null
  preview.value = null
  saveToProfiles.value = false
  errors.name = errors.email = errors.age = null
}

function onSubmit() {
  if (!validate()) return

  const payload = {
    id: Date.now(),
    name: form.name.trim(),
    email: form.email.trim(),
    age: form.age,
    photo: form.photo || null,
  }

  console.log('DatingApp submitted payload:', payload)

  if (saveToProfiles.value) {
    try {
      const key = 'dating:profiles'
      const raw = localStorage.getItem(key)
      const arr = raw ? JSON.parse(raw) : []
      arr.push({ id: payload.id, username: payload.name, isActive: true, liked: false, photo: payload.photo })
      localStorage.setItem(key, JSON.stringify(arr))
      console.log('Saved to localStorage profiles')
    } catch (err) {
      console.warn('Could not save profile to localStorage', err)
    }
  }
}
</script>

<style scoped>
/* small scoped adjustments if needed */
</style>
