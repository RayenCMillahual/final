<script setup>
import { reactive } from 'vue'
import { useAuthStore } from '@/stores/auth'
import { useRouter } from 'vue-router'

const form = reactive({
  username: '',
  password: ''
})

const authStore = useAuthStore()
const router = useRouter()

const handleSubmit = () => {
  if (form.username && form.password) {
    console.log('Iniciar sesión con:', form.username, form.password)
    authStore.login(form.username)
    router.push('/juegos')
  } else {
    console.error('Por favor, ingresa tu usuario y contraseña.')
  }
}
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" placeholder="Usuario" v-model="form.username" />
    <input type="password" placeholder="Contraseña" v-model="form.password" />
    <button type="submit" class="btn-estilos">Iniciar Sesión</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.btn-estilos {
  background-color: red;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;
}
</style>
