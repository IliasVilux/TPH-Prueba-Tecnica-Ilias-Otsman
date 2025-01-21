<script setup>
import { ref } from 'vue';

const props = defineProps({
  mode: {
    type: String,
    required: true
  }
})
const emit = defineEmits(['emitLogin', 'emitRegister'])
const formConfig = {
  login: {
    titulo: 'Inicia sesión',
    boton: 'Iniciar sesión',
    redirectRoute: { name: 'register' },
    mensaje: 'No tienes cuenta? Registrate'
  },
  register: {
    titulo: 'Únete',
    boton: 'Registrarse',
    redirectRoute: { name: 'login' },
    mensaje: 'Tienes cuenta? Inicia sesión'
  }
}

const formData = ref({
  email: '',
  password: ''
})

const handleSubmit = () => {
  if (props.mode === 'login') {
    emit('emitLogin', formData.value)
  }
  if (props.mode === 'register') {
    emit('emitRegister', formData.value)
  }
}
</script>

<template>
  <div class="d-flex align-items-center justify-content-center vh-100 position-relative">
    <div class="background-image"></div>

    <form @submit.prevent="handleSubmit" class="bg-white rounded-4 p-5 mx-2 mx-md-0 position-relative">
      <div class="mb-3">
        <h1 class="mb-0 fade-in-up">TPH - Prueba técnica</h1>
        <h4 class="fade-in-up delay-200">{{ formConfig[props.mode].titulo }}</h4>
      </div>
      <div class="mb-3">
        <label class="form-label">Correo</label>
        <input type="email" class="form-control" v-model="formData.email" placeholder="Introduce tu correo" />
      </div>
      <div class="mb-3">
        <label class="form-label">Contraseña</label>
        <input type="password" class="form-control" v-model="formData.password" placeholder="Introduce tu contraseña" />
      </div>
      <slot></slot>
      <div class="d-flex flex-column align-items-center gap-2 mt-3">
        <button type="submit" class="btn btn-primary w-100">{{ formConfig[props.mode].boton }}</button>
        <RouterLink :to="formConfig[props.mode].redirectRoute" class="text-center text-lg-start w-100">
          {{ formConfig[props.mode].mensaje }}
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
