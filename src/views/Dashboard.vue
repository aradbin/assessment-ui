<script setup lang="ts">
import { useAuthStore } from '@/stores/auth'
import { useRouter } from 'vue-router'

const authStore = useAuthStore()
const router = useRouter()

const logout = () => {
  authStore.logout()
  router.push('/login')
}
</script>

<template>
  <div>
    <nav class="bg-gray-800 text-white p-4 flex justify-between">
      <h1 class="text-lg font-bold">Dashboard</h1>
      <button @click="logout" class="btn">Logout</button>
    </nav>
    <main class="p-4">
      <router-view />
    </main>
  </div>
</template>