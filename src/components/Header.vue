<script setup>
import { RouterLink } from 'vue-router'

import { useAuthStore } from '@/stores/auth.js'
import links from '@/utils/links.js'
import Svg from '@/components/Svg.vue'

const authStore = useAuthStore()

const handleLogout = () => {
  authStore.clearToken()
}
</script>

<template>
  <nav class="navbar navbar-expand-lg p-0 mt-0 mt-lg-4 mb-2">
    <div class="container bg-light rounded-pill p-2">
      <RouterLink :to="{ name: 'home' }" class="navbar-brand mx-2 mx-lg-4">
        <h2 class="fs-4 m-0">TPH</h2>
        <p class="fs-6 fw-lighter lh-1 m-0">Prueba técnica</p>
      </RouterLink>

      <button
        class="navbar-toggler border border-0"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <Svg name="menu" />
      </button>

      <div class="collapse navbar-collapse mx-2 mx-lg-0 ms-lg-5 me-lg-2" id="navbarNavAltMarkup">
        <div class="navbar-nav my-4 my-lg-0">
          <RouterLink v-for="(link, index) in links" :key="index" :to="link.to" class="nav-link">
            {{ link.name }}
          </RouterLink>
        </div>

        <div class="ms-auto me-lg-2 mb-2 mb-lg-0">
          <div v-if="authStore.token">
            <a href="#" @click="handleLogout" class="text-dark">Cerrar sesión</a>
          </div>
          <div v-else class="d-flex align-items-center justify-content-between">
            <RouterLink :to="{ name: 'login' }" class="nav-link">
              <p class="mb-0">Iniciar sesión</p>
            </RouterLink>
            <RouterLink :to="{ name: 'register' }">
              <button class="btn btn-primary ms-4">Registrarse</button>
            </RouterLink>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar-toggler:focus {
  outline: none;
  box-shadow: none;
}

@media (max-width: 992px) {
  .navbar {
    background-color: #f8f9fa;
  }

  .container {
    border-radius: 0 !important;
  }
}
</style>
