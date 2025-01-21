<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <header class="position-absolute text-center w-100 z-1">
    <RouterLink :to="{ name: 'home' }">
      <h2 class="fs-4 m-0 text-white mt-4">Inicio</h2>
    </RouterLink>
  </header>
</template>
