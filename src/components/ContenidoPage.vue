<script setup>
import { computed } from 'vue'
import { ArrowLeft, ArrowUpRight, BookOpen, CheckCircle2, HeartPulse, Users, Trophy } from 'lucide-vue-next'

const props = defineProps({
  numeroContenido: {
    type: Number,
    default: 1
  }
})

const emit = defineEmits(['navigate'])

const modulos = {
  1: {
    titulo: 'Introducción al mundo del deporte',
    bajada: 'Comprende qué es el deporte, cómo se relaciona con la actividad física y por qué tiene un papel importante en la sociedad.',
    secciones: [
      {
        numero: '01',
        titulo: '¿Qué es el deporte?',
        icono: Trophy,
        parrafos: [
          'El deporte es una actividad física organizada que se practica siguiendo reglas o normas propias de una disciplina. Para realizarlo se ponen en juego habilidades corporales, esfuerzo, práctica y, en muchos casos, preparación.',
          'Puede practicarse de manera individual o en equipo. También puede tener distintos propósitos: recrearse, aprender, mejorar las capacidades físicas o participar en una competencia. No todas las personas practican deporte con la intención de ganar; muchas lo hacen para disfrutar del movimiento y compartir con otras personas.'
        ],
        puntos: [
          ['Reglas', 'Orientan la práctica y ayudan a que los participantes conozcan cómo se desarrolla cada disciplina.'],
          ['Habilidades', 'Se utilizan capacidades como la coordinación, la fuerza, la velocidad, el equilibrio y la resistencia.'],
          ['Práctica y preparación', 'La repetición y el entrenamiento permiten aprender movimientos y mejorar el desempeño.'],
          ['Propósito', 'Puede ser recreativo, formativo o competitivo, según el contexto y la intención de quienes participan.']
        ]
      },
      {
        numero: '02',
        titulo: 'Diferencia entre deporte y actividad física',
        icono: HeartPulse,
        parrafos: [
          'La actividad física comprende los movimientos que realiza el cuerpo y que requieren un gasto de energía. Está presente en muchas acciones cotidianas, como caminar, bailar, subir escaleras, montar bicicleta o jugar al aire libre.',
          'El deporte, por su parte, es una forma de actividad física que se desarrolla como una disciplina y cuenta con reglas, características y objetivos definidos. Por eso, aunque ambos conceptos están relacionados, no significan lo mismo.'
        ],
        comparacion: true,
        destacado: 'Todo deporte implica actividad física, pero no toda actividad física constituye un deporte.'
      },
      {
        numero: '03',
        titulo: 'Importancia del deporte en la sociedad',
        icono: Users,
        parrafos: [
          'El deporte tiene importancia en la sociedad porque crea espacios para el movimiento, la recreación, el aprendizaje y el encuentro entre personas. Se practica en escuelas, clubes, comunidades y escenarios deportivos, y puede reunir a participantes de diferentes edades y experiencias.',
          'Además de contribuir al desarrollo de capacidades físicas, el deporte ofrece situaciones en las que se aprende a convivir, respetar acuerdos, colaborar y asumir responsabilidades. Estos aportes dependen también de que la práctica se realice en un ambiente seguro, respetuoso e incluyente.'
        ],
        puntos: [
          ['Desarrollo físico', 'Favorece la práctica de capacidades como la fuerza, la resistencia, la coordinación y la movilidad.'],
          ['Convivencia e integración', 'Genera oportunidades para compartir, participar y relacionarse con otras personas.'],
          ['Aprendizaje de valores', 'Permite poner en práctica el respeto, la disciplina, la responsabilidad y la cooperación.'],
          ['Participación comunitaria', 'Puede promover encuentros y actividades recreativas en escuelas y comunidades.']
        ]
      }
    ],
    resumen: [
      'El deporte es una actividad física organizada que se practica con reglas y objetivos propios.',
      'La actividad física incluye movimientos cotidianos; el deporte es una de sus formas organizadas.',
      'El deporte puede contribuir al desarrollo físico, la convivencia, la integración y el aprendizaje de valores.'
    ]
  },
  2: { titulo: 'Tipos de deportes', bajada: 'En este módulo conocerás las principales formas de clasificar las disciplinas deportivas.', secciones: [] },
  3: { titulo: 'Beneficios del deporte', bajada: 'En este módulo exploraremos los aportes físicos, mentales, emocionales y sociales del deporte.', secciones: [] },
  4: { titulo: 'Valores deportivos', bajada: 'En este módulo abordaremos el respeto, la disciplina, el trabajo en equipo, la responsabilidad y el juego limpio.', secciones: [] },
  5: { titulo: 'Práctica deportiva responsable', bajada: 'En este módulo conocerás prácticas básicas para prepararte, cuidarte y participar de manera responsable.', secciones: [] }
}

const modulo = computed(() => modulos[props.numeroContenido] || modulos[1])
const esModuloDesarrollado = computed(() => props.numeroContenido === 1)

function irAActividades() {
  emit('navigate', `actividades-${props.numeroContenido}`)
}
</script>

<template>
  <main class="pagina-contenido">
    <section class="hero-contenido">
      <div class="hero-texto">
        <span class="sobretitulo"><span class="punto-activo"></span> MUNDO DEPORTE / CONTENIDOS</span>
        <p class="numero-modulo">MÓDULO {{ String(numeroContenido).padStart(2, '0') }} <span>— APRENDIZAJE</span></p>
        <h1>{{ modulo.titulo }}<span>.</span></h1>
        <p class="introduccion">{{ modulo.bajada }}</p>
        <div class="hero-meta">
          <span><BookOpen :size="16" /> Lectura de aprendizaje</span>
          <span><CheckCircle2 :size="16" /> Conceptos y ejemplos</span>
        </div>
      </div>
      <div class="hero-sello" aria-hidden="true">
        <div class="sello-circulo"><Trophy :size="48" stroke-width="1.4" /></div>
        <span>APRENDE<br />EN MOVIMIENTO</span>
      </div>
    </section>

    <template v-if="esModuloDesarrollado">
      <section class="secciones-contenido">
        <article
          v-for="seccion in modulo.secciones"
          :key="seccion.numero"
          class="bloque-tema"
        >
          <div class="tema-cabecera">
            <span class="tema-numero">{{ seccion.numero }}</span>
            <div class="tema-titulo">
              <component :is="seccion.icono" :size="21" />
              <h2>{{ seccion.titulo }}</h2>
            </div>
          </div>

          <div class="tema-cuerpo">
            <p v-for="parrafo in seccion.parrafos" :key="parrafo">{{ parrafo }}</p>

            <div v-if="seccion.puntos" class="rejilla-puntos">
              <div v-for="punto in seccion.puntos" :key="punto[0]" class="punto-card">
                <span class="punto-decorativo"></span>
                <div>
                  <h3>{{ punto[0] }}</h3>
                  <p>{{ punto[1] }}</p>
                </div>
              </div>
            </div>

            <div v-if="seccion.comparacion" class="comparacion">
              <div class="comparacion-card">
                <span class="comparacion-etiqueta">EN LA VIDA COTIDIANA</span>
                <h3>Actividad física</h3>
                <p>Caminar, bailar, subir escaleras o montar bicicleta. Son movimientos corporales que implican gasto de energía y no necesariamente siguen reglas deportivas.</p>
              </div>
              <div class="comparacion-card deporte-card">
                <span class="comparacion-etiqueta">DISCIPLINA ORGANIZADA</span>
                <h3>Deporte</h3>
                <p>Fútbol, baloncesto, natación o atletismo. Se practican como disciplinas con reglas, características y objetivos definidos.</p>
              </div>
            </div>

            <blockquote v-if="seccion.destacado" class="idea-clave">
              <span>IDEA CLAVE</span>
              {{ seccion.destacado }}
            </blockquote>
          </div>
        </article>
      </section>

      <section class="resumen-modulo">
        <div class="resumen-icono"><BookOpen :size="22" /></div>
        <div class="resumen-contenido">
          <span class="sobretitulo">PARA RECORDAR</span>
          <h2>Resumen del módulo</h2>
          <ul>
            <li v-for="idea in modulo.resumen" :key="idea">{{ idea }}</li>
          </ul>
        </div>
      </section>
    </template>

    <section v-else class="modulo-pendiente">
      <span class="pendiente-icono"><BookOpen :size="30" /></span>
      <span class="sobretitulo">CONTENIDO EN DESARROLLO</span>
      <h2>Este módulo será desarrollado a continuación.</h2>
      <p>Estamos completando los módulos en el orden establecido en el diseño del OVA. Este apartado conservará su lugar en la navegación y recibirá su material educativo cuando lleguemos a él.</p>
    </section>

    <footer class="pie-contenido">
      <button class="boton-regreso" @click="emit('navigate', 'inicio')">
        <ArrowLeft :size="16" /> VOLVER A INICIO
      </button>
      <button class="boton-actividades" @click="irAActividades">
        IR A ACTIVIDADES <ArrowUpRight :size="17" />
      </button>
    </footer>
  </main>
</template>

<style scoped>
.pagina-contenido {
  --fondo: #101e2b;
  --panel: #193b50;
  --menta: #43d6b0;
  --azul: #5bafcb;
  --blanco: #f4f8f7;
  --texto: #c0d0d8;
  min-height: calc(100vh - 85px);
  padding: 72px max(7%, calc((100% - 1120px) / 2)) 55px;
  background: var(--fondo);
  color: var(--blanco);
  font-family: 'Inter', sans-serif;
}

.hero-contenido {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 40px;
  padding: 0 0 48px;
  border-bottom: 1px solid #ffffff20;
}

.hero-texto { max-width: 790px; }
.sobretitulo, .numero-modulo, .comparacion-etiqueta {
  display: inline-flex;
  align-items: center;
  gap: 9px;
  color: var(--menta);
  font-size: 10px;
  font-weight: 800;
  letter-spacing: 1.7px;
}
.punto-activo { width: 7px; height: 7px; border-radius: 50%; background: var(--menta); box-shadow: 0 0 12px #43d6b088; }
.numero-modulo { display: block; margin: 27px 0 10px; color: var(--azul); }
.numero-modulo span { color: #829ba9; }
h1, h2, h3 { font-family: 'Barlow Condensed', sans-serif; }
.hero-contenido h1 { max-width: 800px; margin: 0; color: var(--blanco); font-size: clamp(44px, 6.5vw, 76px); line-height: .98; letter-spacing: -.8px; }
.hero-contenido h1 span { color: var(--menta); }
.introduccion { max-width: 700px; margin-top: 22px; color: var(--texto); font-size: 15px; line-height: 1.85; }
.hero-meta { display: flex; flex-wrap: wrap; gap: 22px; margin-top: 25px; color: #9db4c0; font-size: 11px; }
.hero-meta span { display: inline-flex; align-items: center; gap: 8px; }
.hero-meta svg { color: var(--menta); }
.hero-sello { flex: 0 0 180px; display: flex; flex-direction: column; align-items: center; gap: 14px; color: #9db4c0; font-size: 9px; font-weight: 800; letter-spacing: 2px; text-align: center; line-height: 1.6; }
.sello-circulo { width: 126px; height: 126px; display: grid; place-items: center; border: 1px solid #43d6b077; border-radius: 50%; color: var(--menta); background: radial-gradient(circle, #43d6b01c, transparent 68%); box-shadow: 0 0 45px #43d6b012; }
.secciones-contenido { display: grid; gap: 25px; margin-top: 40px; }
.bloque-tema { display: grid; grid-template-columns: 235px 1fr; gap: 35px; padding: 34px; border: 1px solid #5bafcb35; border-radius: 15px; background: linear-gradient(135deg, #193b50 0%, #152e40 100%); }
.tema-cabecera { display: flex; flex-direction: column; align-items: flex-start; gap: 20px; }
.tema-numero { color: var(--menta); font-family: 'Barlow Condensed', sans-serif; font-size: 65px; font-weight: 800; line-height: 1; opacity: .9; }
.tema-titulo { display: flex; align-items: flex-start; gap: 10px; color: var(--menta); }
.tema-titulo svg { flex: 0 0 auto; margin-top: 4px; }
.tema-titulo h2 { margin: 0; color: var(--blanco); font-size: 27px; line-height: 1.1; }
.tema-cuerpo > p { margin: 0 0 15px; color: var(--texto); font-size: 14px; line-height: 1.9; }
.rejilla-puntos { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 13px; margin-top: 22px; }
.punto-card { display: flex; gap: 12px; padding: 17px; border: 1px solid #ffffff17; border-radius: 10px; background: #101e2b70; }
.punto-decorativo { flex: 0 0 7px; height: 7px; margin-top: 6px; border-radius: 50%; background: var(--menta); box-shadow: 0 0 10px #43d6b077; }
.punto-card h3 { margin: 0 0 5px; color: var(--blanco); font-size: 19px; }
.punto-card p { margin: 0; color: #aebfc8; font-size: 12px; line-height: 1.65; }
.comparacion { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 14px; margin: 23px 0; }
.comparacion-card { padding: 20px; border: 1px solid #5bafcb55; border-radius: 11px; background: #101e2b80; }
.comparacion-card.deporte-card { border-color: #43d6b066; }
.comparacion-etiqueta { font-size: 8px; color: var(--azul); }
.deporte-card .comparacion-etiqueta { color: var(--menta); }
.comparacion-card h3 { margin: 10px 0 7px; color: var(--blanco); font-size: 25px; }
.comparacion-card p { margin: 0; color: #b4c5cd; font-size: 12px; line-height: 1.7; }
.idea-clave { margin: 20px 0 0; padding: 18px 20px; border-left: 3px solid var(--menta); border-radius: 0 9px 9px 0; background: #43d6b012; color: var(--blanco); font-size: 14px; line-height: 1.7; }
.idea-clave span { display: block; margin-bottom: 5px; color: var(--menta); font-size: 9px; font-weight: 800; letter-spacing: 1.5px; }
.resumen-modulo { display: flex; gap: 20px; margin-top: 28px; padding: 30px; border: 1px solid #43d6b055; border-radius: 14px; background: #43d6b00d; }
.resumen-icono { flex: 0 0 48px; height: 48px; display: grid; place-items: center; border-radius: 12px; background: #43d6b01c; color: var(--menta); }
.resumen-contenido h2 { margin: 8px 0 13px; color: var(--blanco); font-size: 30px; }
.resumen-contenido ul { display: grid; gap: 9px; margin: 0; padding-left: 18px; color: var(--texto); font-size: 13px; line-height: 1.7; }
.modulo-pendiente { max-width: 760px; margin: 50px auto; padding: 45px; border: 1px solid #5bafcb44; border-radius: 15px; background: #193b50; text-align: center; }
.pendiente-icono { display: grid; width: 65px; height: 65px; margin: 0 auto 20px; place-items: center; border: 1px solid #43d6b066; border-radius: 17px; color: var(--menta); }
.modulo-pendiente h2 { margin: 15px 0 10px; color: var(--blanco); font-size: 32px; }
.modulo-pendiente p { color: var(--texto); font-size: 13px; line-height: 1.8; }
.pie-contenido { display: flex; align-items: center; justify-content: space-between; gap: 15px; margin-top: 35px; }
.boton-regreso, .boton-actividades { display: inline-flex; align-items: center; justify-content: center; gap: 10px; padding: 13px 17px; border: 1px solid #43d6b077; border-radius: 8px; font-size: 10px; font-weight: 800; letter-spacing: 1px; cursor: pointer; transition: .25s ease; }
.boton-regreso { background: transparent; color: #b5c6ce; }
.boton-regreso:hover { color: var(--menta); background: #43d6b012; }
.boton-actividades { background: var(--menta); color: #102b30; }
.boton-actividades:hover { transform: translateY(-2px); background: #70e6c8; box-shadow: 0 8px 22px #43d6b02b; }
button:focus-visible { outline: 2px solid var(--azul); outline-offset: 3px; }

@media (max-width: 800px) {
  .pagina-contenido { padding: 50px 6% 40px; }
  .hero-sello { flex-basis: 120px; }
  .sello-circulo { width: 95px; height: 95px; }
  .bloque-tema { grid-template-columns: 1fr; gap: 18px; padding: 25px; }
  .tema-cabecera { flex-direction: row; align-items: center; gap: 16px; }
  .tema-numero { font-size: 48px; }
}
@media (max-width: 560px) {
  .hero-sello { display: none; }
  .hero-contenido { padding-bottom: 32px; }
  .rejilla-puntos, .comparacion { grid-template-columns: 1fr; }
  .bloque-tema { padding: 20px; }
  .resumen-modulo { padding: 20px; }
  .pie-contenido { align-items: stretch; flex-direction: column-reverse; }
  .boton-regreso, .boton-actividades { width: 100%; }
}
</style>
