<template>
  <div class="container">
    <h1>¡DINOSDEVS TE DA LA BIENVENIDA!</h1>

    <h2>¿Qué encontrarás?</h2>
    <div class="feature-container">
      <ul>
        <li>
          <div class="card">
            <div class="card-header">🦕 <strong>Explora el Mundo Jurásico:</strong></div>
            <div class="card-body">Sumergete en un mundo lleno de información emocionante sobre estos majestuosos reptiles prehistóricos.</div>
          </div>
        </li>
        <li>
          <div class="card">
            <div class="card-header">🦖 <strong>Juegos y Retos:</strong></div>
            <div class="card-body">Pon a prueba tu conocimiento en divertidos juegos y gana puntos.</div>
          </div>
        </li>
        <li>
          <div class="card">
            <div class="card-header">🔍 <strong>Realidad Aumentada:</strong></div>
            <div class="card-body">¡Mira a los dinosaurios en 3D en tu propio espacio, como si estuvieran vivos!</div>
          </div>
        </li>
      </ul>
    </div>

    <h2>¿Listo para la aventura?</h2>

    <div class="button-container">
      <button v-if="!isAuthenticated" @click="login">Iniciar sesión</button>
      <button v-if="isAuthenticated" @click="logoutHandler">Cerrar sesión</button>
    </div>
  </div>
</template>

<script>

import { onMounted, computed } from 'vue';
import { useAuthStore } from '../stores/auth';
import { useAuth0 } from '@auth0/auth0-vue';

export default {
  setup() {
    const authStore = useAuthStore();
    const { loginWithRedirect, logout } = useAuth0(); // Obtén los métodos de Auth0

    const login = () => {
      loginWithRedirect({
        appState: {
          targetUrl: '/Dinojuegos',
        },
      });
    };

    const logoutHandler = () => {
      logout({ returnTo: window.location.origin }); // Redirigir después de cerrar sesión
      authStore.logout(); // Actualizar estado en la tienda
    };
    const isAuthenticated = computed(() => authStore.isAuthenticated);

    onMounted(() => {
      authStore.checkAuth(); // Asegúrate de que este método esté bien definido en tu store
    });

    return {
      login,
      logoutHandler,
      isAuthenticated,
    };
  },
};
</script>

<style scoped>
/* Estructura base */
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: url('@/assets/fondoinicio.jpg') no-repeat center center;
  background-size: cover;
  padding: 40px;
  border-radius: 12px;
  animation: fadeIn 1s ease-in;
  font-family: 'Raleway', sans-serif;
  text-align: center;

  /* Centrando con márgenes */
  width: 100%;
  max-width: 1200px; /* Ajusta el valor para cambiar el ancho máximo */
  margin: 0 auto; /* Centrará el contenedor */
  min-height: 100vh;
  box-sizing: border-box;
}


h1 {
  color: #4c9f70; /* Verde más natural y vibrante */
  font-size: 4rem;
  font-weight: bold;
  text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.2);
  margin-bottom: 1.5rem;
  text-shadow:rgba(0, 0, 0, 0.2) 5px 5px 6px;
  animation: fadeIn 1s ease-in-out;
}

h2 {
  color: #6b8e23; /* Verde oliva */
  font-size: 2.5rem;
  font-weight: 600;
  margin-top: 2rem;
  text-align: center;
  animation: fadeIn 1.2s ease-in-out;
  text-shadow:rgba(0, 0, 0, 0.2) 5px 5px 6px;
  animation: fadeIn 1s ease-in-out;
}

/* Estilo de las características */
.feature-container {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 2rem;
  animation: fadeIn 1.5s ease-in-out;
}

ul {
  padding: 0;
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
}

.card {
  background: #8dbf65; /* Verde dinosaurio */
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.card-header {
  font-size: 1.3rem;
  color: #fff;
  font-weight: 600;
}

.card-body {
  font-size: 1.1rem;
  color: #f1f1f1;
  margin-top: 0.5rem;
}

/* Estilo para los botones */
.button-container {
  display: flex;
  gap: 2rem;
  margin-top: 2rem;
  justify-content: center;
}

.btn-estilos {
  background-color: #3e7f3e;
  color: #fff;
  border: none;
  padding: 12px 30px;
  font-size: 1.1rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.btn-estilos:hover {
  background-color: #2c5a2c;
  transform: translateY(-3px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
}

/* Imagen de fondo del dinosaurio */
.image-container {
  margin-top: 3rem;
  position: relative;
}

.imagen-fondo {
  width: 90%;
  max-width: 700px;
  height: auto;
  border-radius: 20px;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.2);
  transition: transform 0.5s ease-in-out;
}

.imagen-fondo:hover {
  transform: scale(1.05);
}

/* Animaciones */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@media (max-width: 768px) {
  h1 {
    font-size: 3rem;
  }

  h2 {
    font-size: 2rem;
  }

  .btn-estilos {
    padding: 10px 20px;
    font-size: 1rem;
  }

  .feature-container {
    flex-direction: column;
    align-items: center;
  }

  .card {
    width: 90%;
  }

  .imagen-fondo {
    width: 100%;
    height: auto;
  }
}
</style>
