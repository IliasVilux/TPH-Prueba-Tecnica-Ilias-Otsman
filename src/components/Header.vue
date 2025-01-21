<script setup>
import { RouterLink } from 'vue-router'

import { useAuthStore } from '@/stores/auth.js'
import links from '@/utils/links.js'

const authStore = useAuthStore()

const handleLogout = () => {
  authStore.clearToken()
}
</script>

<template>
  <header>
    <div>
      <h2>TPH</h2>
      <p>Prueba técnica - Ilias Otsman</p>
    </div>

    <nav>
      <ul>
        <li v-for="(link, index) in links" :key="index">
          <RouterLink :to="link.to">
            <p>{{ link.name }}</p>
          </RouterLink>
        </li>
      </ul>
    </nav>

    <div v-if="authStore.token">
      <button @click="handleLogout">Cerrar sesión</button>
    </div>
    <div v-else>
      <RouterLink :to="{ name: 'login' }">
        <button>Iniciar sesion</button>
      </RouterLink>
      <RouterLink :to="{ name: 'register' }">
        <button>Registrarse</button>
      </RouterLink>
    </div>
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

ul {
  display: flex;
}

li {
  margin: 0 6px;
}
</style>
