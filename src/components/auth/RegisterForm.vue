<script setup>
import { useRouter, RouterLink } from 'vue-router'
import { ref } from 'vue'

import axios from 'axios'

import { useAuthStore } from '@/stores/auth.js'

const router = useRouter()
const authStore = useAuthStore()

const registerData = ref({
  email: '',
  password: '',
})
const error = ref('')

const handleRegister = async () => {
  await axios
    .post('https://reqres.in/api/register', {
      email: registerData.value.email,
      password: registerData.value.password,
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
      @submit.prevent="handleRegister"
      class="bg-white rounded-4 p-5 mx-2 mx-md-0 position-relative"
    >
      <div class="mb-3">
        <h1 class="mb-0">TPH - Prueba técnica</h1>
        <h4>Únete</h4>
      </div>
      <div class="mb-3">
        <label class="form-label">Correo</label>
        <input
          type="email"
          class="form-control"
          v-model="registerData.email"
          placeholder="Introduce tu correo"
          required
        />
      </div>
      <div class="mb-3">
        <label class="form-label">Contraseña</label>
        <input
          type="password"
          class="form-control"
          v-model="registerData.password"
          placeholder="Introduce tu contraseña"
          minlength="6"
          required
        />
      </div>
      <p v-if="error" class="text-danger m-0">{{ error }}</p>
      <div class="d-flex flex-column align-items-center gap-2 mt-3">
        <button type="submit" class="btn btn-primary w-100">Registrarse</button>
        <RouterLink :to="{ name: 'login' }" class="text-center text-lg-start w-100">
          Tienes cuenta? Inicia sesión
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
