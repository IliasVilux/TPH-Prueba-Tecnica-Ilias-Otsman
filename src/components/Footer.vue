<script setup>
import { RouterLink } from 'vue-router'

import links from '@/utils/links.js'
import Svg from '@/components/Svg.vue'
</script>

<template>
    <footer>
        <div class="footer-block">
            <h1>TPH</h1>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quasi, quam.</p>
        </div>

        <div class="footer-links">
            <nav>
                <ul>
                    <li class="list-head">Enlaces de interés:</li>
                    <li v-for="(link, index) in links" :key="index">
                        <RouterLink :to="link.to">
                            <p>{{ link.name }}</p>
                        </RouterLink>
                    </li>
                </ul>
            </nav>

            <nav>
                <a href="https://github.com/IliasVilux/TPH-Prueba-Tecnica-Ilias-Otsman" target="_blank"><Svg
                        name="github" class="icon" /></a>
                <a href="https://www.linkedin.com/in/ilias-otsman/" target="_blank" style="margin: 0.25rem 0;"><Svg
                        name="linkedin" class="icon" /></a>
                <a href="https://ilias-portfolio-dev.onrender.com/" target="_blank"><Svg name="web" class="icon" /></a>
            </nav>
        </div>
    </footer>
</template>

<style scoped>
.footer-block {
    background-color: var(--color-background);
    color: var(--color-text);
    padding: 7rem 1rem;
    text-align: center;
    border-radius: 8px;
    margin-bottom: 4rem;
}

.footer-block h2 {
    color: var(--color-heading);
}

.list-head {
    font-weight: 600;
    margin-bottom: 0.5rem;
}

.footer-links {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

nav a {
    display: block;
}

@media (prefers-color-scheme: dark) {
    .footer-block {
        background: var(--vt-c-white);
        background: radial-gradient(circle at center bottom, var(--vt-c-white) 0%, var(--vt-c-smoke) 50%);
        --color-heading: var(--vt-c-black);
        --color-text: var(--vt-c-black);
    }

    .list-head {
        color: var(--vt-c-somke);
    }
}

@media (prefers-color-scheme: light) {
    .footer-block {
        background: rgba(47, 47, 47, 1);
        background: radial-gradient(circle at center bottom, rgba(47, 47, 47, 1) 0%, var(--vt-c-black) 50%);
        --color-heading: var(--vt-c-white);
        --color-text: var(--vt-c-white);
    }

    .list-head {
        color: var(--vt-c-divider-normal-1);
    }
}
</style>