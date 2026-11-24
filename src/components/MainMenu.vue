
<script setup>
import { ref } from 'vue'
import { ChevronDown, Activity } from 'lucide-vue-next'

const emit = defineEmits(['navigate'])

const desplegarContenidos = ref(false)
const desplegarActividades = ref(false)

function navegar(pantalla) {
  emit('navigate', pantalla)
  desplegarContenidos.value = false
  desplegarActividades.value = false
}
</script>

<template>
  <header class="menu-principal">
    <a href="#" class="marca" @click.prevent="navegar('inicio')">
      <span class="marca-icono">
        <Activity :size="21" />
      </span>
      <span>MUNDO<span class="marca-naranja">DEPORTE.</span></span>
    </a>

    <nav class="navegacion">
      <!-- INICIO -->
      <button class="enlace" @click="navegar('inicio')">
        INICIO
      </button>

      <!-- DESPLEGABLE DE CONTENIDOS -->
      <div class="grupo-menu">
        <button
          class="enlace"
          :class="{ seleccionado: desplegarContenidos }"
          @click="
            desplegarContenidos = !desplegarContenidos;
            desplegarActividades = false
          "
          :aria-expanded="desplegarContenidos"
        >
          CONTENIDOS
          <ChevronDown
            :size="15"
            :class="{ girar: desplegarContenidos }"
          />
        </button>

        <Transition name="desplegar">
          <div v-if="desplegarContenidos" class="submenu">
            <button @click="navegar('contenido-1')">
              <span>01</span> CONTENIDO 1
            </button>

            <button @click="navegar('contenido-2')">
              <span>02</span> CONTENIDO 2
            </button>

            <button @click="navegar('contenido-3')">
              <span>03</span> CONTENIDO 3
            </button>

            <button @click="navegar('contenido-4')">
              <span>04</span> CONTENIDO 4
            </button>

            <button @click="navegar('contenido-5')">
              <span>05</span> CONTENIDO 5
            </button>
          </div>
        </Transition>
      </div>

      <!-- DESPLEGABLE DE ACTIVIDADES -->
      <div class="grupo-menu">
        <button
          class="enlace"
          :class="{ seleccionado: desplegarActividades }"
          @click="
            desplegarActividades = !desplegarActividades;
            desplegarContenidos = false
          "
          :aria-expanded="desplegarActividades"
        >
          ACTIVIDADES
          <ChevronDown
            :size="15"
            :class="{ girar: desplegarActividades }"
          />
        </button>

        <Transition name="desplegar">
          <div v-if="desplegarActividades" class="submenu">
            <button @click="navegar('actividades-1')">
              <span>01</span> ACTIVIDAD 1
            </button>

            <button @click="navegar('actividades-2')">
              <span>02</span> ACTIVIDAD 2
            </button>

            <button @click="navegar('actividades-3')">
              <span>03</span> ACTIVIDAD 3
            </button>

            <button @click="navegar('actividades-4')">
              <span>04</span> ACTIVIDAD 4
            </button>
          </div>
        </Transition>
      </div>

      <!-- CRÉDITOS -->
      <button class="enlace" @click="navegar('creditos')">
        CRÉDITOS
      </button>

      <!-- EVALUACIÓN FINAL -->
      <button
        class="enlace enlace-evaluacion"
        @click="navegar('evaluacion')"
      >
        EVALUACIÓN FINAL
      </button>
    </nav>

    <div class="indicador-ova">
      <span></span>
      OBJETO VIRTUAL DE APRENDIZAJE
    </div>
  </header>
</template>

<style scoped>
.menu-principal {
  min-height: 85px;
  padding: 0 7%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 25px;
  position: relative;
  z-index: 50;
  background: #101820;
  border-bottom: 1px solid #ffffff20;
  color: #f4f2ed;
  font-family: 'Inter', sans-serif;
}

.marca {
  display: flex;
  align-items: center;
  gap: 11px;
  color: white;
  text-decoration: none;
  font-size: 15px;
  font-weight: 900;
  letter-spacing: -1px;
}

.marca-icono {
  width: 38px;
  height: 38px;
  display: grid;
  place-items: center;
  background: #ed9345;
  color: #101820;
  border-radius: 10px;
}

.marca-naranja {
  color: #ed9345;
}

.navegacion {
  display: flex;
  align-items: center;
  gap: 30px;
}

.grupo-menu {
  position: relative;
}

.enlace {
  display: flex;
  align-items: center;
  gap: 7px;
  padding: 12px 8px;
  border: 1px solid transparent;
  background: transparent;
  color: #aab4bd;
  font-size: 10px;
  font-weight: 800;
  letter-spacing: 1.2px;
  cursor: pointer;
  transition: .25s ease;
}

.enlace:hover,
.enlace.seleccionado,
.enlace-evaluacion {
  color: #ed9345;
}

.enlace svg {
  transition: transform .25s ease;
}

.enlace svg.girar {
  transform: rotate(180deg);
}

.submenu {
  position: absolute;
  top: calc(100% + 14px);
  left: 0;
  width: 220px;
  padding: 9px;
  background: #192632;
  border: 1px solid #ed934555;
  border-radius: 12px;
  box-shadow: 0 15px 40px #0008;
}

.submenu button {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 13px;
  padding: 15px 12px;
  background: transparent;
  border: 1px solid transparent;
  border-radius: 7px;
  color: #dce1e5;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: .7px;
  text-align: left;
  cursor: pointer;
  transition: .25s ease;
}

.submenu button span {
  color: #ed9345;
}

.submenu button:hover {
  background: #ed93451c;
  border-color: #ed934555;
  color: #ed9345;
  padding-left: 17px;
}

.indicador-ova {
  display: flex;
  align-items: center;
  gap: 9px;
  color: #8c99a3;
  font-size: 8px;
  letter-spacing: 1px;
}

.indicador-ova span {
  width: 7px;
  height: 7px;
  background: #70c991;
  border-radius: 50%;
}

.desplegar-enter-active,
.desplegar-leave-active {
  transition: opacity .2s ease, transform .2s ease;
}

.desplegar-enter-from,
.desplegar-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

@media (max-width: 800px) {
  .menu-principal {
    padding: 15px 5%;
    flex-wrap: wrap;
  }

  .navegacion {
    gap: 10px;
  }

  .indicador-ova {
    display: none;
  }
}

@media (max-width: 480px) {
  .menu-principal {
    justify-content: center;
  }

  .navegacion {
    width: 100%;
    justify-content: center;
    gap: 8px;
    flex-wrap: wrap;
  }

  .enlace {
    font-size: 9px;
    padding: 10px 5px;
  }

  .submenu {
    width: 190px;
  }
}
</style>
