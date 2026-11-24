
<script setup>
import { ref, computed } from 'vue'

import WelcomeScreen from './components/WelcomeScreen.vue'
import MainMenu from './components/MainMenu.vue'
import PortadaOVA from './components/PortadaOVA.vue'
import ContenidoPage from './pages/ContenidoPage.vue'
import ActividadesPage from './pages/ActividadesPage.vue'
import EvaluacionPage from './pages/EvaluacionPage.vue'
import CreditosPage from './pages/CreditosPage.vue'

// Control de la pantalla de bienvenida.
const mostrarBienvenida = ref(true)

// Control de la página actual.
const pantallaActual = ref('inicio')

// Identifica el contenido seleccionado.
const numeroContenido = computed(() => {
  const coincidencia = pantallaActual.value.match(/-(\d)$/)
  return coincidencia ? Number(coincidencia[1]) : 1
})

// Cambia de página.
function cambiarPantalla(destino) {
  pantallaActual.value = destino
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

// Oculta la bienvenida al entrar.
function entrarAlOVA() {
  mostrarBienvenida.value = false
}
</script>

<template>
  <main class="aplicacion-ova">

    <!-- Menú principal -->
    <MainMenu
      v-if="!mostrarBienvenida"
      @navigate="cambiarPantalla"
    />

    <!-- Portada -->
    <PortadaOVA
      v-if="pantallaActual === 'inicio'"
      @navegar="cambiarPantalla"
    />

    <!-- Páginas de contenidos -->
    <ContenidoPage
      v-else-if="pantallaActual.startsWith('contenido-')"
      :numero-contenido="numeroContenido"
      @navigate="cambiarPantalla"
    />

    <!-- Páginas de actividades -->
    <ActividadesPage
      v-else-if="pantallaActual.startsWith('actividades-')"
      :numero-contenido="numeroContenido"
      @navigate="cambiarPantalla"
    />

    <!-- Evaluación final -->
    <EvaluacionPage
      v-else-if="pantallaActual === 'evaluacion'"
      @navigate="cambiarPantalla"
    />

    <!-- Créditos del OVA -->
    <CreditosPage
      v-else-if="pantallaActual === 'creditos'"
      @navigate="cambiarPantalla"
    />

    <!-- Pantalla de bienvenida original -->
    <Transition name="bienvenida" appear>
      <WelcomeScreen
        v-if="mostrarBienvenida"
        logo="/logo-mundo-deporte-ova.png"
        texto-boton="ENTRAR AL MUNDO DEPORTIVO"
        @entrar="entrarAlOVA"
      />
    </Transition>

  </main>
</template>

<style>
.aplicacion-ova {
  min-height: 100vh;
  background: #101820;
}

.bienvenida-enter-active,
.bienvenida-leave-active {
  transition: opacity .6s ease, transform .6s ease;
}

.bienvenida-leave-to {
  opacity: 0;
  transform: scale(1.03);
}
</style>
