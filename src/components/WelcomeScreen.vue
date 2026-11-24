
<script setup>
import { ref } from 'vue'
import { ArrowRight } from 'lucide-vue-next'

// PROPS: información que recibe este componente.
defineProps({
  logo: {
    type: String,
    default: '/logo-mundo-deporte-ova.png'
  },
  textoBoton: {
    type: String,
    default: 'ENTRAR AL MUNDO DEPORTIVO'
  }
})

// EMITS: evento que enviamos al componente principal.
const emit = defineEmits(['entrar'])

// REACTIVIDAD: posición del cursor para mover la luz del fondo.
const posicion = ref({
  x: 50,
  y: 50
})

function moverLuz(evento) {
  posicion.value = {
    x: (evento.clientX / window.innerWidth) * 100,
    y: (evento.clientY / window.innerHeight) * 100
  }
}

function entrar() {
  emit('entrar')
}
</script>

<template>
  <section
    class="bienvenida"
    :style="{
      '--mouse-x': posicion.x + '%',
      '--mouse-y': posicion.y + '%'
    }"
    @pointermove="moverLuz"
  >
    <!-- Efectos decorativos de fondo -->
    <div class="luz-fondo"></div>
    <div class="anillo anillo-uno"></div>
    <div class="anillo anillo-dos"></div>

    <!-- Contenido central: logo y botón -->
    <div class="contenido-bienvenida">
      <div class="marco-logo">
        <div class="pulso-logo"></div>

        <img
          :src="logo"
          alt="Logo de Mundo Deporte OVA"
          class="logo-ova"
        />
      </div>

      <button
        class="boton-entrada"
        @click="entrar"
      >
        <span>{{ textoBoton }}</span>
        <ArrowRight :size="21" />
      </button>
    </div>

    <div class="linea-inferior"></div>
  </section>
</template>

<style scoped>
.bienvenida {
  position: fixed;
  inset: 0;
  z-index: 1000;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;

  /* Desenfoque de la portada que queda detrás */
  background: rgba(8, 17, 29, 0.76);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);

  isolation: isolate;
}

/* Luz que responde al movimiento del cursor */
.luz-fondo {
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;

  background: radial-gradient(
    circle at var(--mouse-x) var(--mouse-y),
    rgba(243, 154, 66, 0.19),
    transparent 35%
  );

  transition: background 0.15s ease;
}

/* Anillos decorativos */
.anillo {
  position: absolute;
  z-index: 1;
  width: 390px;
  height: 390px;
  border: 1px solid rgba(243, 154, 66, 0.15);
  border-radius: 50%;
  pointer-events: none;
}

.anillo-uno {
  animation: girar 24s linear infinite;
}

.anillo-dos {
  width: 490px;
  height: 490px;
  border-style: dashed;
  opacity: 0.5;
  animation: girar 38s linear infinite reverse;
}

/* Contenido central */
.contenido-bienvenida {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 48px;
  padding: 25px;
}

/* Marco del logo */
.marco-logo {
  position: relative;
  width: clamp(260px, 38vw, 440px);
  aspect-ratio: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;

  background: radial-gradient(
    circle,
    rgba(255, 255, 255, 0.07),
    rgba(255, 255, 255, 0.01) 70%
  );

  box-shadow:
    0 0 60px rgba(243, 154, 66, 0.12),
    inset 0 0 35px rgba(255, 255, 255, 0.04);

  animation:
    aparecerLogo 1.2s ease both,
    flotar 5s ease-in-out 1.2s infinite;
}

.logo-ova {
  position: relative;
  z-index: 2;
  width: 92%;
  height: 92%;
  object-fit: contain;
  filter: drop-shadow(0 12px 25px rgba(0, 0, 0, 0.35));
  transition: transform 0.5s ease;
}

.marco-logo:hover .logo-ova {
  transform: scale(1.07) rotate(-3deg);
}

/* Pulso luminoso */
.pulso-logo {
  position: absolute;
  inset: -12px;
  border: 1px solid rgba(243, 154, 66, 0.45);
  border-radius: 50%;
  animation: pulso 3s ease-out infinite;
}

/* Botón de entrada */
.boton-entrada {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  min-width: 260px;
  padding: 17px 25px;

  color: #101b29;
  background: #f39a42;
  border: 1px solid #f39a42;
  border-radius: 3px;

  font-family: 'Inter', sans-serif;
  font-size: 11px;
  font-weight: 800;
  letter-spacing: 1.8px;

  cursor: pointer;
  transition: all 0.35s ease;
  animation: aparecerBoton 1s ease 0.4s both;
}

.boton-entrada:hover {
  color: #f39a42;
  background: transparent;
  transform: translateY(-5px);
  box-shadow: 0 12px 35px rgba(243, 154, 66, 0.2);
}

.boton-entrada svg {
  transition: transform 0.3s ease;
}

.boton-entrada:hover svg {
  transform: translateX(6px);
}

.boton-entrada:focus-visible {
  outline: 3px solid white;
  outline-offset: 5px;
}

/* Línea inferior */
.linea-inferior {
  position: absolute;
  z-index: 2;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 3px;

  background: linear-gradient(
    90deg,
    transparent,
    #f39a42,
    transparent
  );

  opacity: 0.65;
}

/* Animaciones */
@keyframes girar {
  to {
    transform: rotate(360deg);
  }
}

@keyframes pulso {
  0% {
    transform: scale(0.96);
    opacity: 0.7;
  }

  100% {
    transform: scale(1.18);
    opacity: 0;
  }
}

@keyframes flotar {
  0%, 100% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-12px);
  }
}

@keyframes aparecerLogo {
  from {
    opacity: 0;
    transform: scale(0.75);
  }

  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes aparecerBoton {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Transición al entrar a la portada */
.bienvenida-enter-active,
.bienvenida-leave-active {
  transition:
    opacity 0.85s ease,
    transform 0.85s ease,
    filter 0.85s ease;
}

.bienvenida-enter-from,
.bienvenida-leave-to {
  opacity: 0;
  transform: scale(1.04);
  filter: blur(10px);
}

/* Adaptación a móviles */
@media (max-width: 600px) {
  .anillo-uno {
    width: 280px;
    height: 280px;
  }

  .anillo-dos {
    width: 350px;
    height: 350px;
  }

  .marco-logo {
    width: min(78vw, 340px);
  }

  .contenido-bienvenida {
    gap: 40px;
  }

  .boton-entrada {
    min-width: 240px;
    font-size: 10px;
  }
}

/* Accesibilidad: reducir movimiento */
@media (prefers-reduced-motion: reduce) {
  .anillo,
  .marco-logo,
  .pulso-logo,
  .boton-entrada {
    animation: none;
  }

  .bienvenida-enter-active,
  .bienvenida-leave-active {
    transition-duration: 0.01ms;
  }
}
</style>
