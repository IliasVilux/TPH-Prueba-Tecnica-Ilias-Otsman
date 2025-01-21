<script setup>
import { useRouter, RouterLink } from 'vue-router'
import { ref } from 'vue'

import axios from 'axios'

import { useAuthStore } from '@/stores/auth.js'

const router = useRouter()
const authStore = useAuthStore()

const loginData = ref({
    email: "",
    password: ""
})
const error = ref('')

const handleLogin = async () => {
    await axios.post('https://reqres.in/api/login', {
        email: loginData.value.email,
        password: loginData.value.password
    }).then((response) => {
        authStore.setToken(response.data.token)
        router.push({ name: 'home' })
    }).catch((err) => {
        error.value = err.response?.data?.error
    })
}
</script>

<template>
    <form @submit.prevent="handleLogin">
        <div>
            <input type="email" v-model="loginData.email">
            <input type="password" v-model="loginData.password">
        </div>
        <div>
            <button type="submit">Iniciar sesión</button>
            <p v-if="error">{{ error }}</p>
        </div>
        <RouterLink :to="{ name: 'register' }">
            <a>No tienes cuenta? Registrate</a>
        </RouterLink>
    </form>
</template>