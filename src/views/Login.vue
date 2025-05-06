<script setup lang="ts">
import { ref } from 'vue'
import { useAuthStore } from '@/stores/auth'
import { useRouter } from 'vue-router'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'

const email = ref('')
const password = ref('')
const authStore = useAuthStore()
const router = useRouter()

const login = async () => {
  try {
    await authStore.login({ email: email.value, password: password.value })
    router.push('/')
  } catch (error) {
    console.log(error)
    alert('Login failed. Please check your credentials.')
  }
}
</script>

<template>
  <div class="flex min-h-screen items-center justify-center bg-background text-foreground">
    <Card class="w-full max-w-md">
      <CardHeader>
        <CardTitle class="text-center">Login</CardTitle>
      </CardHeader>
      <CardContent>
        <form @submit.prevent="login" class="space-y-4">
          <!-- Email Input -->
          <div>
            <label for="email" class="block text-sm font-medium mb-1">Email</label>
            <Input id="email" v-model="email" type="email" placeholder="Enter your email" />
          </div>

          <!-- Password Input -->
          <div>
            <label for="password" class="block text-sm font-medium mb-1">Password</label>
            <Input id="password" v-model="password" type="password" placeholder="Enter your password" />
          </div>

          <!-- Login Button -->
          <Button type="submit" class="w-full">Login</Button>
        </form>
      </CardContent>
    </Card>
  </div>
</template>