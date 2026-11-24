<script setup>
import { computed, ref } from 'vue'

const emit = defineEmits(['navigate'])

const preguntas = [
  {
    modulo: 'MÓDULO 1 · INTRODUCCIÓN AL DEPORTE',
    pregunta: '¿Qué característica permite reconocer una actividad como deporte?',
    opciones: [
      'Que se realice siempre de manera individual.',
      'Que tenga reglas y una práctica organizada.',
      'Que no requiera movimiento corporal.',
      'Que su único propósito sea ganar dinero.'
    ],
    correcta: 1,
    explicacion: 'El deporte es una práctica física organizada que se desarrolla siguiendo reglas y puede tener fines recreativos o competitivos.'
  },
  {
    modulo: 'MÓDULO 1 · INTRODUCCIÓN AL DEPORTE',
    pregunta: '¿Cuál es una diferencia entre deporte y actividad física?',
    opciones: [
      'El deporte suele tener reglas y organización; la actividad física incluye movimientos corporales más amplios.',
      'La actividad física siempre es competitiva y el deporte nunca lo es.',
      'Son exactamente lo mismo en todos los casos.',
      'El deporte no implica movimiento corporal.'
    ],
    correcta: 0,
    explicacion: 'La actividad física comprende movimientos del cuerpo; el deporte es una práctica más estructurada, con reglas y, en muchos casos, competencia.'
  },
  {
    modulo: 'MÓDULO 2 · TIPOS DE DEPORTES',
    pregunta: '¿Cuál de los siguientes es un deporte colectivo?',
    opciones: ['Natación individual', 'Tenis individual', 'Baloncesto', 'Atletismo individual'],
    correcta: 2,
    explicacion: 'El baloncesto es colectivo porque dos equipos participan y colaboran para alcanzar un objetivo común.'
  },
  {
    modulo: 'MÓDULO 2 · TIPOS DE DEPORTES',
    pregunta: '¿Qué tipo de deporte es la natación?',
    opciones: ['De combate', 'Acuático', 'De precisión', 'Colectivo en todos sus formatos'],
    correcta: 1,
    explicacion: 'La natación se clasifica como deporte acuático porque se practica en el agua. Puede tener pruebas individuales y de relevos.'
  },
  {
    modulo: 'MÓDULO 3 · BENEFICIOS DEL DEPORTE',
    pregunta: '¿Cuál es uno de los principales beneficios físicos del deporte?',
    opciones: [
      'Evitar cualquier movimiento corporal.',
      'Mejorar la condición física.',
      'Eliminar la necesidad de descansar.',
      'Impedir el desarrollo de habilidades motrices.'
    ],
    correcta: 1,
    explicacion: 'La práctica deportiva puede mejorar la condición física y contribuir al desarrollo de capacidades como la resistencia, la fuerza y la coordinación.'
  },
  {
    modulo: 'MÓDULO 3 · BENEFICIOS DEL DEPORTE',
    pregunta: '¿Qué beneficio social puede favorecer la práctica deportiva?',
    opciones: [
      'El aislamiento de los participantes.',
      'La falta de comunicación.',
      'La convivencia y la cooperación.',
      'La eliminación de las normas comunes.'
    ],
    correcta: 2,
    explicacion: 'El deporte puede generar espacios de encuentro, comunicación, convivencia y cooperación con otras personas.'
  },
  {
    modulo: 'MÓDULO 4 · VALORES DEPORTIVOS',
    pregunta: '¿Qué significa Fair Play?',
    opciones: [
      'Competir sin reglas.',
      'Juego limpio y respeto.',
      'Ganar a cualquier costo.',
      'Evitar trabajar en equipo.'
    ],
    correcta: 1,
    explicacion: 'Fair Play significa juego limpio: respetar las reglas, a los compañeros, a los adversarios y a quienes participan en la actividad.'
  },
  {
    modulo: 'MÓDULO 4 · VALORES DEPORTIVOS',
    pregunta: 'Un jugador reconoce una falta que cometió, aunque el árbitro no la haya visto. ¿Qué valor demuestra?',
    opciones: ['Irresponsabilidad', 'Falta de disciplina', 'Honestidad y juego limpio', 'Desinterés por el equipo'],
    correcta: 2,
    explicacion: 'Reconocer una falta demuestra honestidad, responsabilidad y respeto por las reglas del juego.'
  },
  {
    modulo: 'MÓDULO 5 · PRÁCTICA DEPORTIVA RESPONSABLE',
    pregunta: '¿Qué debemos hacer antes de comenzar una actividad deportiva intensa?',
    opciones: [
      'Evitar hidratarnos.',
      'Comenzar al máximo esfuerzo.',
      'Realizar un calentamiento.',
      'No movernos.'
    ],
    correcta: 2,
    explicacion: 'El calentamiento prepara progresivamente el cuerpo para la actividad y ayuda a reducir el riesgo de lesiones.'
  },
  {
    modulo: 'MÓDULO 5 · PRÁCTICA DEPORTIVA RESPONSABLE',
    pregunta: '¿Cuál es una práctica responsable durante y después del ejercicio?',
    opciones: [
      'Ignorar la sed y el cansancio.',
      'Usar implementos inadecuados.',
      'Evitar los periodos de descanso.',
      'Mantenerse hidratado y respetar el descanso.'
    ],
    correcta: 3,
    explicacion: 'La hidratación, el uso adecuado de implementos y el descanso son aspectos importantes para practicar deporte de forma responsable.'
  }
]

const respuestas = ref({})
const evaluacionFinalizada = ref(false)

const respondidas = computed(() => Object.keys(respuestas.value).length)
const todasRespondidas = computed(() => respondidas.value === preguntas.length)
const aciertos = computed(() => preguntas.reduce((total, pregunta, indice) => {
  return total + (respuestas.value[indice] === pregunta.correcta ? 1 : 0)
}, 0))
const porcentaje = computed(() => Math.round((aciertos.value / preguntas.length) * 100))
const nota = computed(() => (aciertos.value / preguntas.length * 5).toFixed(1))
const mensajeResultado = computed(() => {
  if (porcentaje.value >= 90) return '¡Excelente trabajo! Tienes un dominio muy sólido de los temas.'
  if (porcentaje.value >= 70) return '¡Buen trabajo! Has comprendido la mayoría de los conceptos.'
  if (porcentaje.value >= 50) return 'Vas por buen camino. Repasa los temas en los que tuviste dudas.'
  return 'Te recomendamos volver a los módulos y realizar nuevamente la evaluación.'
})

function seleccionarRespuesta(indicePregunta, indiceOpcion) {
  if (evaluacionFinalizada.value) return
  respuestas.value = { ...respuestas.value, [indicePregunta]: indiceOpcion }
}

function finalizarEvaluacion() {
  if (todasRespondidas.value) evaluacionFinalizada.value = true
}

function reiniciarEvaluacion() {
  respuestas.value = {}
  evaluacionFinalizada.value = false
}

function claseOpcion(indicePregunta, indiceOpcion) {
  if (!evaluacionFinalizada.value) {
    return respuestas.value[indicePregunta] === indiceOpcion ? 'opcion seleccionada' : 'opcion'
  }

  const esCorrecta = preguntas[indicePregunta].correcta === indiceOpcion
  const fueSeleccionada = respuestas.value[indicePregunta] === indiceOpcion

  if (esCorrecta) return 'opcion correcta'
  if (fueSeleccionada) return 'opcion incorrecta'
  return 'opcion bloqueada'
}
</script>

<template>
  <main class="pagina-evaluacion">
    <section class="hero-evaluacion">
      <div class="hero-texto">
        <span class="sobrelinea">MUNDO DEPORTE / COMPROBACIÓN DEL APRENDIZAJE</span>
        <h1>¿Cuánto sabes <span>de deporte?</span></h1>
        <p>
          Llegó el momento de poner a prueba lo aprendido. Responde las preguntas
          sobre los cinco módulos y descubre cuánto has avanzado.
        </p>
        <div class="datos-evaluacion">
          <span><strong>10</strong> preguntas</span>
          <span><strong>5</strong> módulos</span>
          <span><strong>1</strong> intento por sesión</span>
        </div>
      </div>
      <div class="figura-deportiva" aria-hidden="true">
        <div class="aro aro-uno"></div>
        <div class="aro aro-dos"></div>
        <div class="pelota">✦</div>
        <span class="figura-numero">01—05</span>
      </div>
    </section>

    <section class="panel-evaluacion">
      <div class="barra-superior">
        <div>
          <span class="sobrelinea">TU PROGRESO</span>
          <h2>Evaluación general</h2>
        </div>
        <span class="contador">{{ respondidas }} / {{ preguntas.length }} RESPONDIDAS</span>
      </div>

      <div class="progreso" aria-label="Progreso de respuestas">
        <span :style="{ width: `${respondidas / preguntas.length * 100}%` }"></span>
      </div>

      <div v-if="!evaluacionFinalizada" class="instruccion">
        <span class="punto-info">i</span>
        Selecciona una sola respuesta por pregunta. Puedes cambiarla antes de finalizar.
      </div>

      <article
        v-for="(pregunta, indice) in preguntas"
        :key="indice"
        class="pregunta-card"
      >
        <div class="pregunta-meta">
          <span class="numero-pregunta">{{ String(indice + 1).padStart(2, '0') }}</span>
          <span class="modulo-pregunta">{{ pregunta.modulo }}</span>
          <span v-if="evaluacionFinalizada" class="estado-respuesta" :class="respuestas[indice] === pregunta.correcta ? 'estado-bien' : 'estado-mal'">
            {{ respuestas[indice] === pregunta.correcta ? 'CORRECTA' : 'REVISAR' }}
          </span>
        </div>

        <h3>{{ pregunta.pregunta }}</h3>

        <div class="opciones-grid">
          <button
            v-for="(opcion, indiceOpcion) in pregunta.opciones"
            :key="indiceOpcion"
            type="button"
            :class="claseOpcion(indice, indiceOpcion)"
            :disabled="evaluacionFinalizada"
            @click="seleccionarRespuesta(indice, indiceOpcion)"
          >
            <span class="letra-opcion">{{ ['A', 'B', 'C', 'D'][indiceOpcion] }}</span>
            <span>{{ opcion }}</span>
            <span v-if="evaluacionFinalizada && indiceOpcion === pregunta.correcta" class="marca-opcion">✓</span>
          </button>
        </div>

        <div v-if="evaluacionFinalizada" class="explicacion-respuesta">
          <strong>APRENDIZAJE CLAVE</strong>
          <p>{{ pregunta.explicacion }}</p>
        </div>
      </article>

      <div v-if="!evaluacionFinalizada" class="cierre-evaluacion">
        <div>
          <strong>¿Ya revisaste tus respuestas?</strong>
          <p v-if="!todasRespondidas">Te faltan {{ preguntas.length - respondidas }} pregunta(s) por responder.</p>
          <p v-else>Ya puedes finalizar y conocer tu resultado.</p>
        </div>
        <button class="boton-finalizar" :disabled="!todasRespondidas" @click="finalizarEvaluacion">
          FINALIZAR EVALUACIÓN <span>↗</span>
        </button>
      </div>

      <section v-else class="resultado-final">
        <div class="resultado-circulo">
          <strong>{{ porcentaje }}%</strong>
          <span>DE ACIERTOS</span>
        </div>
        <div class="resultado-texto">
          <span class="sobrelinea">EVALUACIÓN COMPLETADA · NOTA {{ nota }} / 5.0</span>
          <h2>{{ aciertos }} de {{ preguntas.length }} respuestas correctas</h2>
          <p>{{ mensajeResultado }}</p>
          <div class="acciones-resultado">
            <button class="boton-finalizar" @click="reiniciarEvaluacion">VOLVER A INTENTAR <span>↻</span></button>
            <button class="boton-enlace" @click="emit('navigate', 'inicio')">VOLVER AL INICIO ↗</button>
          </div>
        </div>
      </section>
    </section>

    <footer class="pie-evaluacion">
      <span>MUNDO DEPORTE</span>
      <p>Aprender, practicar y crecer a través del deporte.</p>
    </footer>
  </main>
</template>

<style scoped>
.pagina-evaluacion {
  min-height: calc(100vh - 85px);
  padding: 74px 8% 45px;
  background: #101e2b;
  color: #f4f8f7;
  font-family: 'Inter', sans-serif;
}

.hero-evaluacion {
  max-width: 1250px;
  margin: 0 auto 55px;
  display: grid;
  grid-template-columns: 1.35fr .65fr;
  align-items: center;
  gap: 35px;
}

.sobrelinea {
  color: #43d6b0;
  font-size: 9px;
  font-weight: 800;
  letter-spacing: 2px;
}

.hero-texto h1 {
  max-width: 760px;
  margin: 18px 0;
  color: #f2a66a;
  font-family: 'Barlow Condensed', 'Inter', sans-serif;
  font-size: clamp(48px, 7vw, 82px);
  font-weight: 800;
  line-height: .98;
  letter-spacing: -1.5px;
  text-transform: uppercase;
}

.hero-texto h1 span { color: #f4f8f7; }
.hero-texto p { max-width: 650px; color: #bfd0d5; font-size: 14px; line-height: 1.85; }

.datos-evaluacion { display: flex; flex-wrap: wrap; gap: 22px; margin-top: 27px; }
.datos-evaluacion span { color: #9fb5bf; font-size: 10px; letter-spacing: .5px; }
.datos-evaluacion strong { margin-right: 5px; color: #43d6b0; font-size: 17px; }

.figura-deportiva { min-height: 230px; position: relative; display: grid; place-items: center; overflow: hidden; }
.aro { position: absolute; border: 1px solid #43d6b04a; border-radius: 50%; transform: rotate(-28deg); }
.aro-uno { width: 210px; height: 145px; }
.aro-dos { width: 265px; height: 185px; border-color: #f2a66a55; transform: rotate(38deg); }
.pelota { width: 112px; height: 112px; display: grid; place-items: center; border-radius: 50%; background: radial-gradient(circle at 35% 30%, #f2a66a, #d9783e 72%); color: #101e2b; font-size: 45px; box-shadow: 0 20px 55px #0007, inset -10px -12px 22px #8f482d66; }
.figura-numero { position: absolute; right: 7%; bottom: 5px; color: #76909c; font-size: 10px; letter-spacing: 3px; }

.panel-evaluacion { max-width: 1250px; margin: 0 auto; padding: 34px; background: #152b3b; border: 1px solid #ffffff17; border-radius: 18px; box-shadow: 0 25px 65px #0003; }
.barra-superior { display: flex; justify-content: space-between; align-items: end; gap: 20px; }
.barra-superior h2 { margin: 8px 0 0; color: #f4f8f7; font-size: 23px; }
.contador { color: #43d6b0; font-size: 9px; font-weight: 800; letter-spacing: 1.3px; }
.progreso { height: 5px; margin: 22px 0 20px; overflow: hidden; border-radius: 8px; background: #ffffff12; }
.progreso span { display: block; height: 100%; border-radius: inherit; background: linear-gradient(90deg, #43d6b0, #f2a66a); transition: width .3s ease; }
.instruccion { display: flex; align-items: center; gap: 10px; margin-bottom: 25px; color: #a9bdc5; font-size: 11px; }
.punto-info { width: 19px; height: 19px; display: grid; place-items: center; border: 1px solid #43d6b0; border-radius: 50%; color: #43d6b0; font-weight: 800; }

.pregunta-card { padding: 27px 0 30px; border-top: 1px solid #ffffff17; }
.pregunta-meta { display: flex; flex-wrap: wrap; align-items: center; gap: 12px; }
.numero-pregunta { color: #f2a66a; font-size: 12px; font-weight: 900; letter-spacing: 1px; }
.modulo-pregunta { color: #43d6b0; font-size: 8px; font-weight: 800; letter-spacing: 1.25px; }
.estado-respuesta { margin-left: auto; font-size: 8px; font-weight: 900; letter-spacing: 1px; }
.estado-bien { color: #43d6b0; }
.estado-mal { color: #ff9a8c; }
.pregunta-card h3 { margin: 14px 0 18px; color: #f4f8f7; font-size: clamp(16px, 2vw, 19px); line-height: 1.5; }
.opciones-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.opcion { min-height: 58px; padding: 10px 14px; display: flex; align-items: center; gap: 12px; border: 1px solid #ffffff1c; border-radius: 9px; background: #193b50; color: #c8d7db; font: inherit; font-size: 11px; line-height: 1.5; text-align: left; cursor: pointer; transition: border-color .2s ease, background .2s ease, transform .2s ease; }
.opcion:hover:not(:disabled) { border-color: #43d6b0; transform: translateY(-2px); }
.opcion.seleccionada { border-color: #43d6b0; background: #43d6b018; color: #f4f8f7; }
.letra-opcion { width: 25px; height: 25px; flex: 0 0 25px; display: grid; place-items: center; border-radius: 7px; background: #ffffff10; color: #f2a66a; font-size: 10px; font-weight: 900; }
.opcion.seleccionada .letra-opcion { background: #43d6b0; color: #101e2b; }
.opcion.correcta { border-color: #43d6b0; background: #43d6b018; color: #f4f8f7; }
.opcion.correcta .letra-opcion { background: #43d6b0; color: #101e2b; }
.opcion.incorrecta { border-color: #ff8d7d; background: #ff8d7d12; color: #ffd1ca; }
.opcion.incorrecta .letra-opcion { background: #ff8d7d; color: #101e2b; }
.opcion.bloqueada { opacity: .55; cursor: default; }
.opcion:disabled { cursor: default; }
.marca-opcion { margin-left: auto; color: #43d6b0; font-size: 17px; font-weight: 900; }
.explicacion-respuesta { margin-top: 14px; padding: 13px 16px; border-left: 2px solid #43d6b0; background: #43d6b00c; }
.explicacion-respuesta strong { color: #43d6b0; font-size: 8px; letter-spacing: 1.3px; }
.explicacion-respuesta p { margin: 6px 0 0; color: #b8cbd1; font-size: 11px; line-height: 1.7; }

.cierre-evaluacion { display: flex; justify-content: space-between; align-items: center; gap: 20px; margin-top: 18px; padding-top: 25px; border-top: 1px solid #ffffff17; }
.cierre-evaluacion strong { color: #f4f8f7; font-size: 13px; }
.cierre-evaluacion p { margin: 6px 0 0; color: #9fb5bf; font-size: 10px; }
.boton-finalizar { padding: 14px 19px; display: inline-flex; align-items: center; gap: 15px; border: 1px solid #f2a66a; border-radius: 7px; background: #f2a66a; color: #101e2b; font-size: 9px; font-weight: 900; letter-spacing: 1px; cursor: pointer; transition: .2s ease; }
.boton-finalizar:hover:not(:disabled) { background: transparent; color: #f2a66a; }
.boton-finalizar:disabled { opacity: .4; cursor: not-allowed; }
.boton-finalizar span { font-size: 16px; }

.resultado-final { display: flex; align-items: center; gap: 28px; margin-top: 25px; padding: 28px; border: 1px solid #43d6b04a; border-radius: 13px; background: #43d6b00c; }
.resultado-circulo { width: 112px; height: 112px; flex: 0 0 112px; display: flex; flex-direction: column; align-items: center; justify-content: center; border: 5px solid #43d6b0; border-radius: 50%; }
.resultado-circulo strong { color: #f4f8f7; font-size: 27px; }
.resultado-circulo span { color: #43d6b0; font-size: 7px; font-weight: 900; letter-spacing: 1px; }
.resultado-texto h2 { margin: 8px 0; color: #f4f8f7; font-size: 23px; }
.resultado-texto p { color: #b8cbd1; font-size: 12px; line-height: 1.7; }
.acciones-resultado { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 17px; }
.boton-enlace { padding: 12px 15px; border: 1px solid #43d6b05c; border-radius: 7px; background: transparent; color: #43d6b0; font-size: 9px; font-weight: 900; letter-spacing: 1px; cursor: pointer; }
.boton-enlace:hover { background: #43d6b014; }
.pie-evaluacion { max-width: 1250px; margin: 35px auto 0; display: flex; justify-content: space-between; gap: 20px; color: #718994; font-size: 9px; letter-spacing: 1px; }
.pie-evaluacion span { color: #f2a66a; font-weight: 900; }
.pie-evaluacion p { margin: 0; letter-spacing: 0; }

@media (max-width: 760px) {
  .pagina-evaluacion { padding: 50px 5% 35px; }
  .hero-evaluacion { grid-template-columns: 1fr; margin-bottom: 35px; }
  .figura-deportiva { min-height: 150px; }
  .aro-uno { width: 180px; height: 120px; }
  .aro-dos { width: 220px; height: 150px; }
  .pelota { width: 85px; height: 85px; }
  .panel-evaluacion { padding: 22px 17px; }
  .opciones-grid { grid-template-columns: 1fr; }
  .cierre-evaluacion { align-items: stretch; flex-direction: column; }
  .boton-finalizar { justify-content: center; }
  .resultado-final { align-items: flex-start; flex-direction: column; padding: 20px; }
  .pie-evaluacion { flex-direction: column; }
}


/* AJUSTES VISUALES: títulos menta y mejor separación */
.pagina-evaluacion h1,
.pagina-evaluacion h2,
.pagina-evaluacion h3,
.pagina-evaluacion h4 {
  color: #43d6b0 !important;
}
.pagina-evaluacion .hero-texto h1 {
  margin: 23px 0 25px;
  line-height: 1.06;
}
.pagina-evaluacion .barra-superior h2,
.pagina-evaluacion .resultado-texto h2 {
  margin-top: 12px;
  margin-bottom: 15px;
  line-height: 1.25;
}
.pagina-evaluacion .pregunta-card h3 {
  margin: 19px 0 22px;
  line-height: 1.6;
}

</style>
