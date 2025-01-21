<script setup>
import { RouterLink } from 'vue-router'

import links from '@/utils/links.js'
import Svg from '@/components/Svg.vue'
</script>

<template>
  <footer class="bg-light py-5 mt-5">
    <div class="container">
      <section class="d-md-flex justify-content-between align-items-center">
        <div>
          <RouterLink :to="{ name: 'home' }" class="">
            <h2 class="fs-4 m-0">TPH</h2>
            <p class="fs-6 fw-lighter lh-1 m-0">Prueba técnica</p>
          </RouterLink>
          <p class="m-0 mt-3 fs-6 fw-lighter col-md-8">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure iusto cumque ut corrupti
            ipsam porro. Nulla sunt sed reprehenderit nisi quaerat sequi fugiat architecto placeat?
          </p>
        </div>

        <!-- Línea divisoria -->
        <div class="d-md-none border-top my-3"></div>

        <!-- Enlaces sociales -->
        <div class="d-flex gap-3 gap-md-2 align-items-center justify-content-center">
          <a href="https://github.com/IliasVilux/TPH-Prueba-Tecnica-Ilias-Otsman" target="_blank"
            ><Svg name="github" class="icon"
          /></a>
          <a
            href="https://www.linkedin.com/in/ilias-otsman/"
            target="_blank"
            style="margin: 0.25rem 0"
            ><Svg name="linkedin" class="icon"
          /></a>
          <a href="https://ilias-portfolio-dev.onrender.com/" target="_blank"
            ><Svg name="web" class="icon"
          /></a>
        </div>
      </section>

      <!-- Línea divisoria -->
      <div class="d-flex border-top mt-3 mb-4"></div>

      <div>
        <h6>Enlaces de interés:</h6>
        <RouterLink
          v-for="(link, index) in links"
          :key="index"
          :to="link.to"
          class="text-decoration-none text-dark"
        >
          <p class="m-0">{{ link.name }}</p>
        </RouterLink>
      </div>
    </div>
  </footer>
</template>

<style scoped></style>
