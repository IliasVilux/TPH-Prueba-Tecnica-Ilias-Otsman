<script setup>
import { useRouter, RouterLink } from 'vue-router'
import { ref } from 'vue'

import axios from 'axios'

import { useAuthStore } from '@/stores/auth.js'

const router = useRouter()
const authStore = useAuthStore()

const registerData = ref({
    email: "",
    password: ""
})
const error = ref('')

const handleRegister = async () => {
    await axios.post('https://reqres.in/api/register', {
        email: registerData.value.email,
        password: registerData.value.password
    }).then((response) => {
        authStore.setToken(response.data.token)
        router.push({ name: 'home' })
    }).catch((err) => {
        error.value = err.response?.data?.error
    })
}
</script>

<template>
    <form @submit.prevent="handleRegister">
        <div>
            <input type="email" v-model="registerData.email" required>
            <input type="password" v-model="registerData.password" minlength="6">
        </div>
        <div>
            <button type="submit">Registrarse</button>
            <p v-if="error">{{ error }}</p>
        </div>
        <RouterLink :to="{ name: 'login' }">
            <a>Tienes cuenta? Inicia sesion</a>
        </RouterLink>
    </form>
</template>