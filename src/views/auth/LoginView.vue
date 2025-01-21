<script setup>
import { useRouter } from 'vue-router'
import { ref } from 'vue'
import axios from 'axios'

import { useAuthStore } from '@/stores/auth.js'
import HeaderSimple from '@/components/HeaderSimple.vue'
import AuthForm from '@/components/auth/AuthForm.vue'

const router = useRouter()
const authStore = useAuthStore()
const error = ref('')

const handleLogin = async (formData) => {
  await axios
    .post('https://reqres.in/api/login', {
      ...formData
    })
    .then((response) => {
      authStore.setToken(response.data.token)
      router.push({ name: 'home' })
    })
    .catch((err) => {
      error.value = err.response?.data?.error
    })
}
</script>

<template>
  <main>
    <HeaderSimple />
    <AuthForm mode="login" @emitLogin="handleLogin">
      <p v-if="error" class="text-danger m-0">{{ error }}</p>
    </AuthForm>
  </main>
</template>

<style></style>
