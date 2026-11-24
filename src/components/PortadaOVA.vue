
<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

import {
  ArrowUpRight,
  Sparkles,
  Activity,
  ChevronLeft,
  ChevronRight,
  MoveDown,
  Trophy,
  Target,
  Zap
} from 'lucide-vue-next'

// Comunicación con App.vue para cambiar de página.
const emit = defineEmits(['navegar'])

// Disciplinas del carrusel.
const deportes = [
  {
    nombre: 'Fútbol',
    categoria: 'DEPORTE COLECTIVO',
    imagen: 'https://ichef.bbci.co.uk/ace/ws/549/cpsprodpb/B5B9/production/_92212564_gettyimages-185933155.jpg.webp',
    numero: '01'
  },
  {
    nombre: 'Baloncesto',
    categoria: 'DEPORTE COLECTIVO',
    imagen: 'https://img.olympics.com/images/image/private/t_16-9_640/f_auto/v1538355600/primary/jfvf9vxukhdmuxoh2xcz',
    numero: '02'
  },
  {
    nombre: 'Natación',
    categoria: 'DEPORTE ACUÁTICO',
    imagen: 'https://images.unsplash.com/photo-1530549387789-4c1017266635?auto=format&fit=crop&w=1200&q=85',
    numero: '03'
  },
  {
    nombre: 'Atletismo',
    categoria: 'DEPORTE INDIVIDUAL',
    imagen: 'https://www.endondecorrer.com/wp-content/uploads/2020/04/Pruebas-oficiales-de-atletismo-696x465.jpg',
    numero: '04'
  }
]

// Estado del carrusel.
const indice = ref(0)
const deporteActual = computed(() => deportes[indice.value])

// Posición y estado del cursor.
const cursorX = ref(-100)
const cursorY = ref(-100)
const cursorActivo = ref(false)

let temporizador
let observador

// Pasar al siguiente deporte.
function siguiente() {
  indice.value = (indice.value + 1) % deportes.length
}

// Regresar al deporte anterior.
function anterior() {
  indice.value = (indice.value - 1 + deportes.length) % deportes.length
}

// Seleccionar un deporte directamente.
function seleccionarDeporte(i) {
  indice.value = i
}

// Navegar al primer contenido del OVA.
function explorar() {
  emit('navegar', 'contenido-1')
}

// Efecto del cursor personalizado.
function moverCursor(evento) {
  if (evento.pointerType === 'touch') return

  cursorX.value = evento.clientX
  cursorY.value = evento.clientY

  cursorActivo.value = Boolean(
    evento.target.closest(
      'button, a, .imagen-contenedor, .tarjeta-editorial'
    )
  )
}

function salirCursor() {
  cursorActivo.value = false
}

// Inicialización de animaciones y carrusel.
onMounted(() => {
  temporizador = setInterval(siguiente, 5000)

  window.addEventListener('pointermove', moverCursor)
  window.addEventListener('pointerout', salirCursor)

  if ('IntersectionObserver' in window) {
    observador = new IntersectionObserver((entradas) => {
      entradas.forEach((entrada) => {
        if (entrada.isIntersecting) {
          entrada.target.classList.add('visible')
          observador.unobserve(entrada.target)
        }
      })
    }, {
      threshold: 0.12
    })

    document.querySelectorAll('.revelar').forEach((elemento) => {
      observador.observe(elemento)
    })
  } else {
    document.querySelectorAll('.revelar').forEach((elemento) => {
      elemento.classList.add('visible')
    })
  }
})

// Limpieza de eventos y temporizadores.
onUnmounted(() => {
  clearInterval(temporizador)
  observador?.disconnect()

  window.removeEventListener('pointermove', moverCursor)
  window.removeEventListener('pointerout', salirCursor)
})
</script>

<template>
  <main class="portada">

    <!-- CURSOR PERSONALIZADO -->
    <div
      class="cursor-personalizado"
      :class="{ activo: cursorActivo }"
      :style="{ left: cursorX + 'px', top: cursorY + 'px' }"
    >
      <span></span>
    </div>

    <!-- FONDO -->
    <div class="fondo-grid"></div>
    <div class="luz-fondo"></div>

    <!-- PORTADA PRINCIPAL -->
    <section class="contenido" id="inicio">

      <div class="texto-principal">

        <div class="numero-editorial">
          <span>01</span>
          <div></div>
          <span>UNA NUEVA FORMA DE EXPLORAR</span>
        </div>

        <div class="etiqueta">
          <Sparkles :size="15" />
          <span>EL MOVIMIENTO NOS UNE</span>
        </div>

        <h1>
          EL DEPORTE
          <span>ES</span>
          <span class="titulo-destacado">UNIVERSO.</span>
        </h1>

        <p class="descripcion">
          Mucho más que una actividad física. Un espacio para
          descubrir disciplinas, comprender el movimiento y
          explorar todo lo que hace del deporte una experiencia
          extraordinaria.
        </p>

        <div class="acciones">

          <button class="boton-principal" @click="explorar">
            <span>EXPLORAR EL OVA</span>
            <ArrowUpRight :size="19" />
          </button>

          <a href="#experiencia" class="boton-secundario">
            CONOCE MÁS
            <MoveDown :size="16" />
          </a>

        </div>

        <div class="frase">
          <span>APRENDE</span>
          <i></i>
          <span>CONOCE</span>
          <i></i>
          <span>VIVE</span>
        </div>

      </div>

      <!-- CARRUSEL -->
      <div class="visual" id="deportes">

        <div class="rotulo-vertical">
          MUNDO DEPORTE — EXPLORA SIN LÍMITES
        </div>

        <div class="imagen-contenedor">

          <div class="marco-imagen"></div>

          <Transition name="cambiar-foto" mode="out-in">
            <img
              :key="deporteActual.imagen"
              :src="deporteActual.imagen"
              :alt="'Fotografía de ' + deporteActual.nombre"
              class="imagen-deporte"
            />
          </Transition>

          <div class="sombra-imagen"></div>

          <div class="etiqueta-fotografia">
            <span class="punto-naranja"></span>
            DISCIPLINA DESTACADA
          </div>

          <div class="informacion-imagen">
            <span>{{ deporteActual.categoria }}</span>
            <h2>{{ deporteActual.nombre }}</h2>
            <p>DESCUBRE SU ESENCIA.</p>
          </div>

          <div class="contador">
            <span>{{ deporteActual.numero }}</span>
            <span class="contador-linea"></span>
            <span>04</span>
          </div>

          <div class="marca-agua">
            {{ deporteActual.numero }}
          </div>

        </div>

        <div class="controles">

          <div class="texto-control">
            <span>EXPLORA LAS DISCIPLINAS</span>

            <div class="indicadores">
              <button
                v-for="(deporte, i) in deportes"
                :key="deporte.numero"
                class="indicador"
                :class="{ activo: indice === i }"
                :aria-label="'Mostrar ' + deporte.nombre"
                @click="seleccionarDeporte(i)"
              ></button>
            </div>
          </div>

          <div class="flechas">
            <button aria-label="Anterior" @click="anterior">
              <ChevronLeft :size="19" />
            </button>

            <button aria-label="Siguiente" @click="siguiente">
              <ChevronRight :size="19" />
            </button>
          </div>

        </div>

      </div>

    </section>

    <!-- FRANJA EDITORIAL -->
    <section class="franja-editorial">

      <div>
        <span>01 /</span>
        <p>DESCUBRIMIENTO</p>
      </div>

      <div>
        <span>02 /</span>
        <p>CONOCIMIENTO</p>
      </div>

      <div>
        <span>03 /</span>
        <p>MOVIMIENTO</p>
      </div>

      <div class="franja-icono">
        <Activity :size="23" />
      </div>

    </section>

    <!-- SEGUNDA SECCIÓN -->
    <section class="experiencia" id="experiencia">

      <div class="experiencia-cabecera revelar">

        <div>
          <span class="sobrelinea">MÁS QUE DEPORTE</span>

          <h2>
            UNA EXPERIENCIA
            <span>EN MOVIMIENTO.</span>
          </h2>
        </div>

        <p>
          El deporte conecta personas, desarrolla habilidades
          y abre un mundo de posibilidades. Este es el comienzo
          de un recorrido por su universo.
        </p>

      </div>

      <div class="tarjetas-editoriales">

        <article class="tarjeta-editorial revelar">

          <div class="tarjeta-numero">01</div>

          <div class="tarjeta-icono">
            <Trophy :size="25" />
          </div>

          <span class="tarjeta-etiqueta">SUPERACIÓN</span>

          <h3>DISCIPLINA</h3>

          <p>
            Cada deporte representa retos, constancia y
            oportunidades para desarrollar nuevas capacidades.
          </p>

          <div class="tarjeta-pie">
            <span>DESCUBRE TU POTENCIAL</span>
            <ArrowUpRight :size="19" />
          </div>

        </article>

        <article class="tarjeta-editorial tarjeta-central revelar">

          <div class="tarjeta-numero">02</div>

          <div class="tarjeta-icono">
            <Target :size="25" />
          </div>

          <span class="tarjeta-etiqueta">CONOCIMIENTO</span>

          <h3>APRENDIZAJE</h3>

          <p>
            Comprender el deporte también significa conocer
            sus características, sus reglas y su diversidad.
          </p>

          <div class="tarjeta-pie">
            <span>AMPLÍA TUS HORIZONTES</span>
            <ArrowUpRight :size="19" />
          </div>

        </article>

        <article class="tarjeta-editorial revelar">

          <div class="tarjeta-numero">03</div>

          <div class="tarjeta-icono">
            <Zap :size="25" />
          </div>

          <span class="tarjeta-etiqueta">ENERGÍA</span>

          <h3>MOVIMIENTO</h3>

          <p>
            Explorar diferentes disciplinas permite descubrir
            nuevas formas de vivir y experimentar el deporte.
          </p>

          <div class="tarjeta-pie">
            <span>VIVE LA EXPERIENCIA</span>
            <ArrowUpRight :size="19" />
          </div>

        </article>

      </div>

      <!-- CITA EDITORIAL -->
      <div class="cita-editorial revelar">

        <span class="comilla">“</span>

        <p>
          EL MOVIMIENTO ES EL COMIENZO DE GRANDES DESCUBRIMIENTOS.
        </p>

        <span class="cita-firma">
          MUNDO DEPORTE / 2026
        </span>

      </div>

    </section>

    <!-- PIE DE PÁGINA -->
    <footer class="pie">

      <a href="#inicio" class="logo logo-pie">

        <span class="logo-icono">
          <Activity :size="19" />
        </span>

        <span class="logo-texto">
          MUNDO<span>DEPORTE.</span>
        </span>

      </a>

      <span>UNA EXPERIENCIA PARA TODOS</span>

      <span class="pie-final">
        DESCUBRE TU POTENCIAL
        <ArrowUpRight :size="15" />
      </span>

    </footer>

  </main>
</template>

<style scoped>
/* =================================
   CONFIGURACIÓN GENERAL
================================= */

* {
  box-sizing: border-box;
}

.portada {
  --fondo: #101820;
  --fondo-claro: #17232e;
  --naranja: #ed9345;
  --blanco: #f4f2ed;
  --gris: #9ba5ad;

  min-height: 100vh;
  padding: 0 7%;
  background: var(--fondo);
  color: var(--blanco);
  position: relative;
  overflow: hidden;
  font-family: 'Inter', sans-serif;
}

html {
  scroll-behavior: smooth;
}

::selection {
  background: var(--naranja);
  color: var(--fondo);
}

/* =================================
   FONDO Y PROFUNDIDAD
================================= */

.fondo-grid {
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: .12;

  background-image:
    linear-gradient(to right, #ffffff 1px, transparent 1px),
    linear-gradient(to bottom, #ffffff 1px, transparent 1px);

  background-size: 100px 100px;

  mask-image: linear-gradient(
    to bottom,
    black,
    transparent 85%
  );
}

.luz-fondo {
  position: absolute;
  width: 500px;
  height: 500px;
  border-radius: 50%;
  background: var(--naranja);
  filter: blur(180px);
  opacity: .10;
  top: 12%;
  right: 4%;
  pointer-events: none;
  animation: luz 9s ease-in-out infinite alternate;
}

/* =================================
   CURSOR PERSONALIZADO
================================= */

.cursor-personalizado {
  position: fixed;
  width: 35px;
  height: 35px;
  border: 1px solid #ed9345;
  border-radius: 50%;
  pointer-events: none;
  z-index: 1000;
  transform: translate(-50%, -50%);

  transition:
    width .25s ease,
    height .25s ease,
    background .25s ease,
    opacity .25s ease;

  opacity: .65;
}

.cursor-personalizado span {
  position: absolute;
  width: 5px;
  height: 5px;
  background: var(--naranja);
  border-radius: 50%;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.cursor-personalizado.activo {
  width: 55px;
  height: 55px;
  background: #ed934522;
  opacity: 1;
}

/* =================================
   PORTADA PRINCIPAL
================================= */

.contenido {
  max-width: 1350px;
  min-height: 690px;

  display: grid;
  grid-template-columns: .92fr 1.08fr;
  align-items: center;

  gap: 75px;
  margin: 0 auto;
  padding: 70px 0 85px;

  position: relative;
  z-index: 2;
}

.texto-principal {
  animation: entrada 1s ease both;
}

.numero-editorial {
  display: flex;
  align-items: center;
  gap: 13px;

  color: #788590;
  font-size: 8px;
  letter-spacing: 1.6px;
  margin-bottom: 45px;
}

.numero-editorial span:first-child {
  color: var(--naranja);
  font-size: 12px;
  font-weight: 800;
}

.numero-editorial div {
  width: 35px;
  height: 1px;
  background: var(--naranja);
}

.etiqueta {
  display: flex;
  align-items: center;
  gap: 10px;

  color: var(--naranja);
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 2.5px;
}

h1 {
  font-family: 'Barlow Condensed', sans-serif;
  font-size: clamp(70px, 8.2vw, 116px);
  font-weight: 900;
  line-height: .83;
  letter-spacing: -3px;
  margin: 30px 0;
}

h1 span {
  display: block;
}

.titulo-destacado {
  color: var(--naranja);
  margin-top: 8px;
}

.descripcion {
  max-width: 425px;
  color: #aab4bd;
  font-size: 13px;
  line-height: 2;
  margin-top: 33px;
}

/* =================================
   BOTONES PRINCIPALES
================================= */

.acciones {
  display: flex;
  align-items: center;
  gap: 27px;
  margin-top: 34px;
  flex-wrap: wrap;
}

.boton-principal {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 35px;

  padding: 17px 20px;

  background: var(--naranja);
  color: var(--fondo);

  border: 1px solid var(--naranja);
  border-radius: 7px;

  font-size: 9px;
  font-weight: 900;
  letter-spacing: 1.1px;

  cursor: pointer;

  transition: .3s ease;
}

.boton-principal:hover {
  background: transparent;
  color: var(--naranja);
  transform: translateY(-4px);
  box-shadow: 0 12px 30px #ed934522;
}

.boton-principal svg {
  transition: transform .3s ease;
}

.boton-principal:hover svg {
  transform: translate(4px, -4px);
}

.boton-secundario {
  display: flex;
  align-items: center;
  gap: 10px;

  padding: 10px 0;

  color: var(--blanco);
  text-decoration: none;

  font-size: 9px;
  font-weight: 700;
  letter-spacing: 1px;

  transition: color .3s ease;
}

.boton-secundario:hover {
  color: var(--naranja);
}

.boton-secundario svg {
  transition: transform .3s ease;
}

.boton-secundario:hover svg {
  transform: translateY(5px);
}

.frase {
  display: flex;
  align-items: center;
  gap: 13px;

  margin-top: 55px;

  color: #778590;
  font-size: 9px;
  letter-spacing: 2px;
}

.frase i {
  width: 4px;
  height: 4px;
  background: var(--naranja);
  border-radius: 50%;
}

/* =================================
   CARRUSEL EDITORIAL
================================= */

.visual {
  position: relative;
  padding: 0 15px 15px 0;
  perspective: 1000px;
}

.imagen-contenedor {
  height: 490px;
  width: 100%;

  position: relative;
  overflow: hidden;

  background: #263541;
  border: 1px solid #ffffff22;
  border-radius: 10px;

  z-index: 2;
  cursor: none;
}

.marco-imagen {
  position: absolute;
  inset: 12px;
  border: 1px solid #ffffff55;
  border-radius: 6px;
  z-index: 4;
  pointer-events: none;
}

.imagen-deporte {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 1s ease;
}

.imagen-contenedor:hover .imagen-deporte {
  transform: scale(1.055);
}

.sombra-imagen {
  position: absolute;
  inset: 0;

  background: linear-gradient(
    to top,
    rgba(8, 15, 22, .94),
    rgba(8, 15, 22, .10) 55%,
    rgba(8, 15, 22, .15)
  );

  pointer-events: none;
}

.etiqueta-fotografia {
  position: absolute;
  top: 30px;
  left: 32px;

  display: flex;
  align-items: center;
  gap: 10px;

  color: white;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 1.5px;
}

.punto-naranja {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--naranja);
  box-shadow: 0 0 10px #ed934588;
}

.informacion-imagen {
  position: absolute;
  bottom: 43px;
  left: 35px;
  z-index: 3;
}

.informacion-imagen span {
  color: var(--naranja);
  font-size: 9px;
  letter-spacing: 2px;
  font-weight: 700;
}

.informacion-imagen h2 {
  font-family: 'Barlow Condensed', sans-serif;
  font-size: clamp(42px, 5vw, 65px);
  text-transform: uppercase;
  line-height: .95;
  margin: 12px 0 7px;
}

.informacion-imagen p {
  color: #c1c9cf;
  font-size: 8px;
  letter-spacing: 2px;
}

.contador {
  position: absolute;
  top: 31px;
  right: 33px;
  z-index: 3;

  display: flex;
  align-items: center;
  gap: 9px;

  font-size: 12px;
  font-weight: 800;
}

.contador span:first-child {
  color: var(--naranja);
  font-size: 19px;
}

.contador span:last-child {
  color: #ffffff99;
}

.contador-linea {
  width: 25px;
  height: 1px;
  background: #ffffff77;
}

.marca-agua {
  position: absolute;
  right: 20px;
  bottom: -45px;

  font-family: 'Barlow Condensed', sans-serif;
  font-size: 200px;
  font-weight: 900;
  line-height: 1;

  color: #ffffff12;
  z-index: 2;
  pointer-events: none;
}

.rotulo-vertical {
  position: absolute;
  right: -32px;
  top: 40%;

  writing-mode: vertical-rl;

  color: #7e8994;
  font-size: 8px;
  letter-spacing: 2px;
  z-index: 5;
}

/* =================================
   CONTROLES DEL CARRUSEL
================================= */

.controles {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 24px;
}

.texto-control {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.texto-control > span {
  font-size: 8px;
  color: #85919c;
  letter-spacing: 1.5px;
}

.indicadores {
  display: flex;
  align-items: center;
  gap: 9px;
}

.indicador {
  width: 24px;
  height: 4px;

  background: #53616e;
  border: 1px solid transparent;
  border-radius: 5px;

  cursor: pointer;
  transition: .3s ease;
}

.indicador:hover {
  background: #ffffff;
}

.indicador.activo {
  width: 48px;
  background: var(--naranja);
  border-color: var(--naranja);
}

.flechas {
  display: flex;
  gap: 8px;
}

.flechas button {
  width: 42px;
  height: 42px;

  display: grid;
  place-items: center;

  color: white;
  border: 1px solid #ffffff45;
  border-radius: 8px;

  background: transparent;
  cursor: pointer;

  transition: .3s ease;
}

.flechas button:hover {
  color: var(--fondo);
  background: var(--naranja);
  border-color: var(--naranja);
  transform: translateY(-3px);
}

/* =================================
   FRANJA EDITORIAL
================================= */

.franja-editorial {
  border-top: 1px solid #ffffff22;
  border-bottom: 1px solid #ffffff22;

  display: grid;
  grid-template-columns: repeat(3, 1fr) 60px;
  align-items: center;

  padding: 25px 0;
  position: relative;
  z-index: 2;
}

.franja-editorial > div:not(.franja-icono) {
  display: flex;
  align-items: center;
  gap: 15px;
}

.franja-editorial span {
  color: var(--naranja);
  font-size: 10px;
  font-weight: 800;
}

.franja-editorial p {
  color: #c2c9ce;
  font-size: 9px;
  letter-spacing: 1.5px;
}

.franja-icono {
  color: var(--naranja);
  display: flex;
  justify-content: flex-end;
}

/* =================================
   SEGUNDA SECCIÓN
================================= */

.experiencia {
  max-width: 1350px;
  margin: 0 auto;
  padding: 125px 0 100px;
  position: relative;
  z-index: 2;
}

.experiencia-cabecera {
  display: grid;
  grid-template-columns: 1.2fr .8fr;
  gap: 80px;
  align-items: end;
  margin-bottom: 55px;
}

.sobrelinea {
  color: var(--naranja);
  font-size: 9px;
  font-weight: 800;
  letter-spacing: 2.5px;
}

.experiencia-cabecera h2 {
  font-family: 'Barlow Condensed', sans-serif;
  font-size: clamp(45px, 6vw, 78px);
  line-height: .9;
  letter-spacing: -1px;
  margin-top: 20px;
}

.experiencia-cabecera h2 span {
  display: block;
  color: var(--naranja);
}

.experiencia-cabecera > p {
  max-width: 390px;
  color: #aab4bd;
  font-size: 12px;
  line-height: 2;
  padding-bottom: 7px;
}

/* =================================
   TARJETAS EDITORIALES
================================= */

.tarjetas-editoriales {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.tarjeta-editorial {
  position: relative;
  min-height: 310px;
  padding: 30px;

  background: #17232e;
  border: 1px solid #ffffff25;
  border-radius: 12px;

  display: flex;
  flex-direction: column;
  overflow: hidden;

  transition:
    transform .35s ease,
    background .35s ease,
    border-color .35s ease,
    box-shadow .35s ease;
}

.tarjeta-editorial::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 3px;
  background: var(--naranja);
  transition: width .4s ease;
}

.tarjeta-editorial:hover {
  transform: translateY(-9px);
  background: #202f3b;
  border-color: #ed934580;
  box-shadow: 0 18px 35px #0003;
}

.tarjeta-editorial:hover::before {
  width: 100%;
}

.tarjeta-central {
  background: #ed9345;
  color: var(--fondo);
  border-color: #f3a45f;
}

.tarjeta-central:hover {
  background: #f3a45f;
  border-color: #ffc28b;
}

.tarjeta-numero {
  position: absolute;
  top: 18px;
  right: 25px;

  color: #ffffff17;
  font-family: 'Barlow Condensed', sans-serif;
  font-size: 65px;
  font-weight: 900;
}

.tarjeta-icono {
  width: 48px;
  height: 48px;

  border: 1px solid #ffffff40;
  border-radius: 9px;

  display: grid;
  place-items: center;

  color: var(--naranja);
  margin-bottom: 35px;
}

.tarjeta-central .tarjeta-icono {
  color: var(--fondo);
  border-color: #10182055;
}

.tarjeta-etiqueta {
  color: var(--naranja);
  font-size: 8px;
  font-weight: 800;
  letter-spacing: 2px;
}

.tarjeta-central .tarjeta-etiqueta {
  color: #101820aa;
}

.tarjeta-editorial h3 {
  font-family: 'Barlow Condensed', sans-serif;
  font-size: 34px;
  margin: 7px 0 10px;
}

.tarjeta-editorial > p {
  color: #aab4bd;
  font-size: 11px;
  line-height: 1.8;
  max-width: 280px;
}

.tarjeta-central > p {
  color: #27333d;
}

.tarjeta-pie {
  margin-top: auto;
  padding-top: 25px;

  display: flex;
  align-items: center;
  justify-content: space-between;

  color: var(--naranja);
  font-size: 8px;
  font-weight: 800;
  letter-spacing: 1px;
}

.tarjeta-central .tarjeta-pie {
  color: var(--fondo);
}

.tarjeta-pie svg {
  transition: transform .3s ease;
}

.tarjeta-editorial:hover .tarjeta-pie svg {
  transform: translate(4px, -4px);
}

/* =================================
   CITA EDITORIAL
================================= */

.cita-editorial {
  margin-top: 100px;
  padding: 60px 25px;

  border-top: 1px solid #ffffff20;
  border-bottom: 1px solid #ffffff20;

  text-align: center;
}

.comilla {
  display: block;
  color: var(--naranja);
  font-family: Georgia, serif;
  font-size: 65px;
  line-height: .7;
}

.cita-editorial p {
  max-width: 750px;
  margin: 20px auto;

  font-family: 'Barlow Condensed', sans-serif;
  font-size: clamp(28px, 4vw, 45px);
  font-weight: 800;
  letter-spacing: 1px;
}

.cita-firma {
  color: #8995a0;
  font-size: 8px;
  letter-spacing: 2px;
}

/* =================================
   PIE DE PÁGINA
================================= */

.pie {
  min-height: 90px;
  border-top: 1px solid #ffffff20;

  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;

  position: relative;
  z-index: 2;
}

.logo {
  display: flex;
  align-items: center;
  gap: 11px;
  text-decoration: none;
  color: var(--blanco);
}

.logo-icono {
  width: 39px;
  height: 39px;

  display: grid;
  place-items: center;

  background: var(--naranja);
  color: var(--fondo);
  border-radius: 50%;
}

.logo-texto {
  font-size: 15px;
  font-weight: 900;
  letter-spacing: -1px;
}

.logo-texto span {
  color: var(--naranja);
}

.logo-pie .logo-icono {
  width: 30px;
  height: 30px;
}

.logo-pie .logo-texto {
  font-size: 12px;
}

.pie > span {
  color: #8995a0;
  font-size: 8px;
  letter-spacing: 1.5px;
}

.pie-final {
  display: flex;
  align-items: center;
  gap: 8px;
}

/* =================================
   TRANSICIONES
================================= */

.cambiar-foto-enter-active,
.cambiar-foto-leave-active {
  transition:
    opacity .65s ease,
    transform .65s ease;
}

.cambiar-foto-enter-from {
  opacity: 0;
  transform: scale(1.06);
}

.cambiar-foto-leave-to {
  opacity: 0;
  transform: scale(.96);
}

.revelar {
  opacity: 0;
  transform: translateY(35px);

  transition:
    opacity .8s ease,
    transform .8s ease;
}

.revelar.visible {
  opacity: 1;
  transform: translateY(0);
}

/* =================================
   ANIMACIONES
================================= */

@keyframes entrada {
  from {
    opacity: 0;
    transform: translateY(35px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes luz {
  from {
    transform: scale(.8);
  }

  to {
    transform: scale(1.2);
  }
}

/* =================================
   RESPONSIVE
================================= */

@media (max-width: 1000px) {
  .portada {
    padding: 0 5%;
  }

  .contenido {
    gap: 40px;
    grid-template-columns: .9fr 1.1fr;
  }

  .imagen-contenedor {
    height: 420px;
  }
}

@media (max-width: 750px) {
  .contenido {
    grid-template-columns: 1fr;
    gap: 55px;
    padding: 65px 0;
  }

  h1 {
    font-size: clamp(70px, 15vw, 105px);
  }

  .numero-editorial {
    margin-bottom: 35px;
  }

  .imagen-contenedor {
    height: 400px;
  }

  .rotulo-vertical {
    display: none;
  }

  .experiencia {
    padding: 85px 0;
  }

  .experiencia-cabecera {
    grid-template-columns: 1fr;
    gap: 25px;
  }

  .tarjetas-editoriales {
    grid-template-columns: 1fr;
  }

  .tarjeta-editorial {
    min-height: 280px;
  }

  .franja-editorial {
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  .franja-icono {
    display: none;
  }

  .cursor-personalizado {
    display: none;
  }
}

@media (max-width: 480px) {
  .portada {
    padding: 0 6%;
  }

  .numero-editorial {
    font-size: 7px;
    gap: 8px;
  }

  h1 {
    font-size: 67px;
  }

  .descripcion {
    font-size: 12px;
  }

  .acciones {
    align-items: flex-start;
    flex-direction: column;
  }

  .imagen-contenedor {
    height: 330px;
  }

  .informacion-imagen {
    left: 23px;
    bottom: 30px;
  }

  .informacion-imagen h2 {
    font-size: 43px;
  }

  .etiqueta-fotografia {
    left: 23px;
    font-size: 7px;
  }

  .marca-agua {
    font-size: 140px;
  }

  .controles {
    gap: 10px;
  }

  .franja-editorial p {
    font-size: 8px;
  }

  .pie {
    padding: 20px 0;
    flex-wrap: wrap;
  }

  .pie > span {
    font-size: 7px;
  }

  .cita-editorial {
    padding: 45px 10px;
  }
}

/* =================================
   ACCESIBILIDAD
================================= */

@media (hover: none) {
  .cursor-personalizado {
    display: none;
  }

  .imagen-contenedor {
    cursor: auto;
  }
}

@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: .01ms !important;
    transition-duration: .01ms !important;
    scroll-behavior: auto !important;
  }

  .revelar {
    opacity: 1;
    transform: none;
  }
}


/* AJUSTES VISUALES: títulos menta y mejor separación */
.portada h1,
.portada h2,
.portada h3,
.portada h4 {
  color: #43d6b0;
}
.portada .contenido h1 {
  margin-top: 24px;
  margin-bottom: 28px;
  line-height: 1.08;
}
.portada .informacion-imagen h2,
.portada .texto-editorial h2 {
  margin-top: 17px;
  margin-bottom: 15px;
  line-height: 1.08;
}
.portada .tarjeta-editorial h3 {
  margin-top: 14px;
  margin-bottom: 12px;
  line-height: 1.25;
}

</style>
