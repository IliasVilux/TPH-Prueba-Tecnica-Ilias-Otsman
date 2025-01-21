<script setup>
import { useRouter, RouterLink } from 'vue-router'
import { ref } from 'vue'

import axios from 'axios'

import { useAuthStore } from '@/stores/auth.js'

const router = useRouter()
const authStore = useAuthStore()

const loginData = ref({
  email: '',
  password: '',
})
const error = ref('')

const handleLogin = async () => {
  await axios
    .post('https://reqres.in/api/login', {
      email: loginData.value.email,
      password: loginData.value.password,
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
  <div class="d-flex align-items-center justify-content-center vh-100 position-relative">
    <div class="background-image"></div>

    <form
      @submit.prevent="handleLogin"
      class="bg-white rounded-4 p-5 mx-2 mx-md-0 position-relative"
    >
      <div class="mb-3">
        <h1 class="mb-0 fade-in-up">TPH - Prueba técnica</h1>
        <h4 class="fade-in-up delay-200">Inicia sesión</h4>
      </div>
      <div class="mb-3">
        <label class="form-label">Correo</label>
        <input
          type="email"
          class="form-control"
          v-model="loginData.email"
          placeholder="Introduce tu correo"
        />
      </div>
      <div class="mb-3">
        <label class="form-label">Contraseña</label>
        <input
          type="password"
          class="form-control"
          v-model="loginData.password"
          placeholder="Introduce tu contraseña"
        />
      </div>
      <p v-if="error" class="text-danger m-0">{{ error }}</p>
      <div class="d-flex flex-column align-items-center gap-2 mt-3">
        <button type="submit" class="btn btn-primary w-100">Iniciar sesión</button>
        <RouterLink :to="{ name: 'register' }" class="text-center text-lg-start w-100">
          No tienes cuenta? Registrate
        </RouterLink>
      </div>
    </form>
  </div>
</template>

<style scoped>
.text-danger::first-letter {
  text-transform: uppercase;
}

.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 58%;
  background-image: url('https://4kwallpapers.com/images/wallpapers/gradient-background-6016x3384-11027.jpg');
  background-size: cover;
  background-position: bottom;
  z-index: -1;
}
</style>
