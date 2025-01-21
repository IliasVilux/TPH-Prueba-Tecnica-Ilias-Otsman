<script setup>
import { RouterLink } from 'vue-router'

import links from '@/utils/links.js'
import Svg from '@/components/Svg.vue'
</script>

<template>
  <footer>
    <div>
      <h1>TPH</h1>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quasi, quam.</p>
    </div>

    <div>
      <nav>
        <ul>
          <li>Enlaces de interés:</li>
          <li v-for="(link, index) in links" :key="index">
            <RouterLink :to="link.to">
              <p>{{ link.name }}</p>
            </RouterLink>
          </li>
        </ul>
      </nav>

      <nav>
        <a href="https://github.com/IliasVilux/TPH-Prueba-Tecnica-Ilias-Otsman" target="_blank"><Svg
            name="github" /></a>
        <a href="https://www.linkedin.com/in/ilias-otsman/" target="_blank" style="margin: 0.25rem 0"><Svg
            name="linkedin" /></a>
        <a href="https://ilias-portfolio-dev.onrender.com/" target="_blank"><Svg name="web" /></a>
      </nav>
    </div>
  </footer>
</template>

<style scoped></style>
