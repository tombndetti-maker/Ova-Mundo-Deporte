<script setup>
import { computed, ref, watch } from 'vue'

const props = defineProps({
  numeroContenido: { type: Number, default: 1 }
})

const emit = defineEmits(['navigate'])

const actividadActiva = ref(0)
const respuestas = ref({ identificar: {}, clasificar: {}, valores: {}, reto: {} })
const revisado = ref({ identificar: false, clasificar: false, valores: false, reto: false })

watch(() => props.numeroContenido, (nuevo) => {
  actividadActiva.value = Math.min(Math.max(nuevo - 1, 0), 3)
}, { immediate: true })

const actividades = [
  { numero: '01', categoria: 'RECONOCIMIENTO VISUAL', titulo: '¿Qué deporte es?', descripcion: 'Observa cada imagen y selecciona el nombre de la disciplina que representa.', icono: '◉', tiempo: '3 MIN' },
  { numero: '02', categoria: 'CLASIFICACIÓN', titulo: 'Organiza las disciplinas', descripcion: 'Relaciona cada deporte con el tipo de práctica al que pertenece.', icono: '▦', tiempo: '4 MIN' },
  { numero: '03', categoria: 'ANÁLISIS DE SITUACIONES', titulo: 'Los valores en acción', descripcion: 'Lee situaciones deportivas y reconoce el valor que se pone en práctica.', icono: '✦', tiempo: '4 MIN' },
  { numero: '04', categoria: 'JUEGO INTERACTIVO', titulo: 'Reto deportivo', descripcion: 'Responde preguntas de los cinco módulos y comprueba cuánto has aprendido.', icono: '⚡', tiempo: '5 MIN' }
]

const preguntasVisuales = [
  { nombre: 'Baloncesto', imagen: 'https://images.unsplash.com/photo-1546519638-68e109498ffc?auto=format&fit=crop&w=900&q=85', opciones: ['Natación', 'Baloncesto', 'Atletismo'], correcta: 'Baloncesto' },
  { nombre: 'Natación', imagen: 'https://images.unsplash.com/photo-1530549387789-4c1017266635?auto=format&fit=crop&w=900&q=85', opciones: ['Ciclismo', 'Tenis', 'Natación'], correcta: 'Natación' },
  { nombre: 'Atletismo', imagen: 'https://images.unsplash.com/photo-1461896836934-ffe607ba8211?auto=format&fit=crop&w=900&q=85', opciones: ['Atletismo', 'Boxeo', 'Fútbol'], correcta: 'Atletismo' },
  { nombre: 'Boxeo', imagen: 'https://images.unsplash.com/photo-1549719386-74dfcbf7dbed?auto=format&fit=crop&w=900&q=85', opciones: ['Voleibol', 'Boxeo', 'Gimnasia'], correcta: 'Boxeo' }
]

const deportes = [
  { nombre: 'Atletismo', correcta: 'Individual' },
  { nombre: 'Fútbol', correcta: 'Colectivo' },
  { nombre: 'Boxeo', correcta: 'Combate' },
  { nombre: 'Natación', correcta: 'Acuático' },
  { nombre: 'Tiro con arco', correcta: 'Precisión' }
]
const tiposDeporte = ['Individual', 'Colectivo', 'Combate', 'Acuático', 'Precisión']

const situaciones = [
  { texto: 'Un jugador ayuda a levantarse a un rival después de una caída, aunque su equipo esté compitiendo.', opciones: ['Respeto', 'Egoísmo', 'Desinterés'], correcta: 'Respeto', explicacion: 'El respeto se demuestra al tratar con consideración a todas las personas, incluso a quienes compiten como rivales.' },
  { texto: 'Un equipo se organiza, se comunica y coopera para alcanzar un objetivo común.', opciones: ['Trabajo en equipo', 'Ventaja individual', 'Falta de compromiso'], correcta: 'Trabajo en equipo', explicacion: 'El trabajo en equipo implica colaborar y coordinar esfuerzos para lograr una meta compartida.' },
  { texto: 'Una deportista cumple las reglas y acepta la decisión del árbitro, aunque no le favorezca.', opciones: ['Juego limpio', 'Irresponsabilidad', 'Rivalidad'], correcta: 'Juego limpio', explicacion: 'El juego limpio consiste en actuar con honestidad, respetar las reglas y aceptar las decisiones.' },
  { texto: 'Un estudiante asiste a sus entrenamientos y mantiene el compromiso con su práctica.', opciones: ['Disciplina', 'Improvisación', 'Descuido'], correcta: 'Disciplina', explicacion: 'La disciplina se refleja en la constancia y el cumplimiento de los compromisos.' }
]

const reto = [
  { pregunta: '¿Qué característica distingue al deporte de muchas actividades físicas cotidianas?', opciones: ['Siempre se practica en un gimnasio', 'Tiene reglas y objetivos establecidos', 'No requiere movimiento corporal', 'Solo puede practicarse profesionalmente'], correcta: 'Tiene reglas y objetivos establecidos', explicacion: 'El deporte suele organizarse mediante reglas, objetivos y formas de participación.' },
  { pregunta: '¿Cuál de estos es un deporte colectivo?', opciones: ['Natación individual', 'Atletismo individual', 'Baloncesto', 'Tiro con arco'], correcta: 'Baloncesto', explicacion: 'El baloncesto se juega entre equipos que cooperan para alcanzar un objetivo común.' },
  { pregunta: '¿Cuál es un beneficio relacionado con la práctica deportiva?', opciones: ['Mejorar la condición física', 'Eliminar la necesidad de descansar', 'Evitar toda interacción social', 'Impedir el aprendizaje de habilidades'], correcta: 'Mejorar la condición física', explicacion: 'La práctica deportiva puede favorecer capacidades físicas y contribuir al bienestar.' },
  { pregunta: '¿Qué significa Fair Play?', opciones: ['Ganar a cualquier costo', 'Competir sin reglas', 'Juego limpio y respeto', 'Evitar trabajar en equipo'], correcta: 'Juego limpio y respeto', explicacion: 'Fair Play significa actuar con honestidad y respetar las reglas, rivales y compañeros.' },
  { pregunta: '¿Qué conviene hacer antes de una actividad deportiva intensa?', opciones: ['Evitar hidratarse', 'Realizar un calentamiento', 'Comenzar al máximo esfuerzo', 'No mover las articulaciones'], correcta: 'Realizar un calentamiento', explicacion: 'El calentamiento prepara progresivamente el cuerpo para la actividad.' }
]

const puntajes = computed(() => ({
  identificar: preguntasVisuales.filter((p, i) => respuestas.value.identificar[i] === p.correcta).length,
  clasificar: deportes.filter((d, i) => respuestas.value.clasificar[i] === d.correcta).length,
  valores: situaciones.filter((s, i) => respuestas.value.valores[i] === s.correcta).length,
  reto: reto.filter((p, i) => respuestas.value.reto[i] === p.correcta).length
}))

function comprobar(clave) {
  revisado.value[clave] = true
}
function reiniciar(clave) {
  respuestas.value[clave] = {}
  revisado.value[clave] = false
}
function seleccionarActividad(indice) {
  actividadActiva.value = indice
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
function siguiente() {
  if (actividadActiva.value < 3) seleccionarActividad(actividadActiva.value + 1)
}
function anterior() {
  if (actividadActiva.value > 0) seleccionarActividad(actividadActiva.value - 1)
}
</script>

<template>
  <main class="pagina-actividades">
    <section class="hero-actividades">
      <div class="hero-texto">
        <span class="sobretitulo"><i></i> MUNDO DEPORTE / ZONA DE APRENDIZAJE</span>
        <h1>Aprender también<br><span>es jugar.</span></h1>
        <p>Explora los retos, observa, relaciona y demuestra lo que sabes sobre el mundo del deporte.</p>
      </div>
      <div class="hero-dato"><strong>04</strong><span>EXPERIENCIAS<br>INTERACTIVAS</span></div>
      <div class="linea-decorativa"></div>
    </section>

    <section class="selector-actividades">
      <div class="selector-cabecera">
        <div><span class="mini-etiqueta">ELIGE TU DESAFÍO</span><h2>Ruta de actividades</h2></div>
        <span class="contador">{{ String(actividadActiva + 1).padStart(2, '0') }} <b>/ 04</b></span>
      </div>
      <div class="ruta-grid">
        <button v-for="(actividad, i) in actividades" :key="actividad.numero" class="ruta-card" :class="{ activa: actividadActiva === i, completada: revisado[['identificar','clasificar','valores','reto'][i]] }" @click="seleccionarActividad(i)">
          <span class="ruta-numero">{{ actividad.numero }}</span><span class="ruta-icono">{{ actividad.icono }}</span>
          <span class="ruta-titulo">{{ actividad.titulo }}</span><span class="ruta-tiempo">{{ actividad.tiempo }} <b>↗</b></span>
        </button>
      </div>
    </section>

    <section class="actividad-panel">
      <div class="panel-cabecera">
        <div><span class="mini-etiqueta">ACTIVIDAD {{ actividades[actividadActiva].numero }} / {{ actividades[actividadActiva].categoria }}</span><h2>{{ actividades[actividadActiva].titulo }}</h2><p>{{ actividades[actividadActiva].descripcion }}</p></div>
        <span class="panel-simbolo">{{ actividades[actividadActiva].icono }}</span>
      </div>

      <div v-if="actividadActiva === 0" class="contenido-actividad">
        <div class="instruccion">OBSERVA LAS IMÁGENES Y ELIGE LA DISCIPLINA CORRECTA</div>
        <div class="visual-grid">
          <article v-for="(item, i) in preguntasVisuales" :key="item.nombre" class="visual-card">
            <div class="visual-imagen"><img :src="item.imagen" :alt="`Deporte: ${item.nombre}`" loading="lazy"><span>0{{ i + 1 }}</span></div>
            <div class="visual-respuesta"><label :for="`visual-${i}`">¿Qué deporte observas?</label><select :id="`visual-${i}`" v-model="respuestas.identificar[i]"><option disabled value="">Selecciona una opción</option><option v-for="opcion in item.opciones" :key="opcion" :value="opcion">{{ opcion }}</option></select>
              <small v-if="revisado.identificar" :class="respuestas.identificar[i] === item.correcta ? 'correcto' : 'incorrecto'">{{ respuestas.identificar[i] === item.correcta ? '✓ ¡Correcto!' : `Respuesta: ${item.correcta}` }}</small>
            </div>
          </article>
        </div>
        <div class="pie-actividad"><span>{{ Object.keys(respuestas.identificar).length }} / 4 respuestas</span><div><button v-if="revisado.identificar" class="btn-reintentar" @click="reiniciar('identificar')">REINTENTAR</button><button class="btn-comprobar" @click="comprobar('identificar')">{{ revisado.identificar ? 'ACTUALIZAR RESULTADO' : 'COMPROBAR RESPUESTAS' }}</button></div></div>
        <div v-if="revisado.identificar" class="resultado">Obtuviste <strong>{{ puntajes.identificar }} de 4</strong> respuestas correctas.</div>
      </div>

      <div v-else-if="actividadActiva === 1" class="contenido-actividad">
        <div class="instruccion">ASIGNA A CADA DISCIPLINA SU CLASIFICACIÓN</div>
        <div class="clasificacion-lista"><div v-for="(deporte, i) in deportes" :key="deporte.nombre" class="clasificacion-fila"><span class="fila-numero">0{{ i + 1 }}</span><strong>{{ deporte.nombre }}</strong><select v-model="respuestas.clasificar[i]"><option disabled value="">Selecciona el tipo</option><option v-for="tipo in tiposDeporte" :key="tipo" :value="tipo">{{ tipo }}</option></select><span v-if="revisado.clasificar" class="marca-respuesta" :class="respuestas.clasificar[i] === deporte.correcta ? 'bien' : 'mal'">{{ respuestas.clasificar[i] === deporte.correcta ? '✓' : '×' }}</span></div></div>
        <p class="nota-ayuda">Recuerda: algunas disciplinas pueden tener modalidades individuales y por equipos. En este ejercicio se utiliza una clasificación representativa.</p>
        <div class="pie-actividad"><span>{{ Object.keys(respuestas.clasificar).length }} / 5 respuestas</span><div><button v-if="revisado.clasificar" class="btn-reintentar" @click="reiniciar('clasificar')">REINTENTAR</button><button class="btn-comprobar" @click="comprobar('clasificar')">{{ revisado.clasificar ? 'ACTUALIZAR RESULTADO' : 'COMPROBAR RESPUESTAS' }}</button></div></div>
        <div v-if="revisado.clasificar" class="resultado">Obtuviste <strong>{{ puntajes.clasificar }} de 5</strong> respuestas correctas.</div>
      </div>

      <div v-else-if="actividadActiva === 2" class="contenido-actividad">
        <div class="instruccion">LEE CADA SITUACIÓN Y RECONOCE EL VALOR DEPORTIVO</div>
        <article v-for="(situacion, i) in situaciones" :key="i" class="situacion-card"><span class="situacion-numero">SITUACIÓN 0{{ i + 1 }}</span><p>{{ situacion.texto }}</p><div class="opciones-situacion"><button v-for="opcion in situacion.opciones" :key="opcion" :class="{ elegida: respuestas.valores[i] === opcion, acierto: revisado.valores && opcion === situacion.correcta, error: revisado.valores && respuestas.valores[i] === opcion && opcion !== situacion.correcta }" @click="respuestas.valores[i] = opcion">{{ opcion }}</button></div><div v-if="revisado.valores" class="explicacion">{{ situacion.explicacion }}</div></article>
        <div class="pie-actividad"><span>{{ Object.keys(respuestas.valores).length }} / 4 respuestas</span><div><button v-if="revisado.valores" class="btn-reintentar" @click="reiniciar('valores')">REINTENTAR</button><button class="btn-comprobar" @click="comprobar('valores')">{{ revisado.valores ? 'ACTUALIZAR RESULTADO' : 'COMPROBAR RESPUESTAS' }}</button></div></div>
        <div v-if="revisado.valores" class="resultado">Obtuviste <strong>{{ puntajes.valores }} de 4</strong> respuestas correctas.</div>
      </div>

      <div v-else class="contenido-actividad">
        <div class="instruccion">CINCO PREGUNTAS PARA PONER A PRUEBA LO APRENDIDO</div>
        <article v-for="(pregunta, i) in reto" :key="i" class="pregunta-reto"><span class="situacion-numero">PREGUNTA 0{{ i + 1 }}</span><h3>{{ pregunta.pregunta }}</h3><div class="opciones-reto"><button v-for="opcion in pregunta.opciones" :key="opcion" :class="{ elegida: respuestas.reto[i] === opcion, acierto: revisado.reto && opcion === pregunta.correcta, error: revisado.reto && respuestas.reto[i] === opcion && opcion !== pregunta.correcta }" @click="respuestas.reto[i] = opcion">{{ opcion }}</button></div><div v-if="revisado.reto" class="explicacion">{{ pregunta.explicacion }}</div></article>
        <div class="pie-actividad"><span>{{ Object.keys(respuestas.reto).length }} / 5 respuestas</span><div><button v-if="revisado.reto" class="btn-reintentar" @click="reiniciar('reto')">REINTENTAR</button><button class="btn-comprobar" @click="comprobar('reto')">{{ revisado.reto ? 'ACTUALIZAR RESULTADO' : 'FINALIZAR RETO' }}</button></div></div>
        <div v-if="revisado.reto" class="resultado resultado-final">Tu resultado: <strong>{{ puntajes.reto }} / 5</strong><span>{{ puntajes.reto === 5 ? '¡Excelente trabajo!' : '¡Sigue practicando, vas por buen camino!' }}</span></div>
      </div>

      <div class="navegacion-actividad"><button :disabled="actividadActiva === 0" @click="anterior">← ANTERIOR</button><span>AVANZA A TU RITMO</span><button :disabled="actividadActiva === 3" @click="siguiente">SIGUIENTE →</button></div>
    </section>

    <section class="cierre-actividades"><div><span class="mini-etiqueta">SIGUIENTE ETAPA</span><h2>¿Listo para comprobar<br>todo lo que aprendiste?</h2></div><button @click="emit('navigate', 'evaluacion')">IR A LA EVALUACIÓN FINAL <span>↗</span></button></section>
    <footer class="pie-pagina"><span>MUNDO DEPORTE.</span><span>APRENDER · MOVERSE · COMPARTIR</span></footer>
  </main>
</template>

<style scoped>
.pagina-actividades{min-height:100vh;background:#101e2b;color:#f4f8f7;font-family:Inter,Arial,sans-serif;padding:0 7% 35px}.hero-actividades{position:relative;display:flex;align-items:center;justify-content:space-between;gap:25px;padding:78px 0 68px;border-bottom:1px solid #ffffff20;overflow:hidden}.sobretitulo,.mini-etiqueta,.instruccion,.situacion-numero{font-size:10px;font-weight:800;letter-spacing:2px;color:#43d6b0}.sobretitulo{display:flex;align-items:center;gap:10px}.sobretitulo i{width:7px;height:7px;border-radius:50%;background:#43d6b0;box-shadow:0 0 13px #43d6b0}.hero-texto h1{font-size:clamp(45px,7vw,82px);line-height:.98;letter-spacing:-4px;margin:23px 0 18px;font-weight:900}.hero-texto h1 span{color:#f2a66a}.hero-texto p,.panel-cabecera p{color:#bfd0d5;line-height:1.8;max-width:560px;font-size:14px}.hero-dato{display:flex;align-items:center;gap:15px;color:#bfd0d5;font-size:9px;letter-spacing:1.5px;line-height:1.6}.hero-dato strong{font-size:76px;line-height:1;color:#43d6b0;letter-spacing:-5px}.linea-decorativa{position:absolute;width:180px;height:180px;border:1px solid #43d6b020;border-radius:50%;right:4%;top:10%;pointer-events:none}.selector-actividades{padding:48px 0 42px}.selector-cabecera{display:flex;justify-content:space-between;align-items:end;margin-bottom:22px}.selector-cabecera h2,.panel-cabecera h2{font-size:27px;margin:8px 0 0;letter-spacing:-1px}.contador{font-size:24px;font-weight:800;color:#f2a66a}.contador b{font-size:13px;color:#718994}.ruta-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px}.ruta-card{position:relative;text-align:left;min-height:160px;padding:19px;background:#193b50;border:1px solid #ffffff13;border-radius:10px;color:#f4f8f7;cursor:pointer;transition:.25s;display:flex;flex-direction:column;align-items:flex-start}.ruta-card:hover,.ruta-card.activa{border-color:#f2a66a;transform:translateY(-3px);background:#20465a}.ruta-numero{font-size:10px;color:#f2a66a;font-weight:800;letter-spacing:1px}.ruta-icono{font-size:23px;color:#43d6b0;margin:14px 0 8px}.ruta-titulo{font-size:14px;font-weight:800}.ruta-tiempo{margin-top:auto;padding-top:12px;font-size:9px;letter-spacing:1.3px;color:#9bb2bb}.ruta-tiempo b{color:#43d6b0;margin-left:5px}.actividad-panel{background:#142d3e;border:1px solid #ffffff19;border-radius:13px;padding:clamp(22px,4vw,42px);}.panel-cabecera{display:flex;justify-content:space-between;align-items:flex-start;gap:20px;padding-bottom:25px;border-bottom:1px solid #ffffff19}.panel-cabecera h2{font-size:clamp(25px,4vw,38px);color:#f2a66a;margin:12px 0 7px}.panel-cabecera p{margin:0}.panel-simbolo{font-size:46px;color:#43d6b0;opacity:.85}.contenido-actividad{padding-top:26px}.instruccion{margin-bottom:20px;color:#bfd0d5}.visual-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:13px}.visual-card{background:#193b50;border:1px solid #ffffff12;border-radius:9px;overflow:hidden}.visual-imagen{height:150px;position:relative;overflow:hidden}.visual-imagen img{width:100%;height:100%;object-fit:cover;transition:transform .5s}.visual-card:hover img{transform:scale(1.06)}.visual-imagen>span{position:absolute;left:12px;top:12px;background:#101e2bd9;color:#43d6b0;padding:6px 8px;font-size:10px;font-weight:800}.visual-respuesta{padding:14px}.visual-respuesta label{display:block;font-size:11px;color:#bfd0d5;margin-bottom:9px}.visual-respuesta select,.clasificacion-fila select{width:100%;background:#102636;color:#f4f8f7;border:1px solid #ffffff25;border-radius:6px;padding:11px;font:inherit;font-size:12px}.correcto{display:block;color:#43d6b0;margin-top:9px}.incorrecto{display:block;color:#f2a66a;margin-top:9px}.pie-actividad{display:flex;justify-content:space-between;align-items:center;gap:15px;margin-top:25px;padding-top:20px;border-top:1px solid #ffffff19;color:#9bb2bb;font-size:11px}.pie-actividad>div{display:flex;gap:9px;flex-wrap:wrap}.btn-comprobar,.btn-reintentar{padding:12px 17px;border-radius:6px;font-size:9px;font-weight:900;letter-spacing:1px;cursor:pointer;transition:.2s}.btn-comprobar{background:#f2a66a;color:#10202b;border:1px solid #f2a66a}.btn-comprobar:hover{background:#ffc08f}.btn-reintentar{background:transparent;color:#43d6b0;border:1px solid #43d6b0}.resultado{margin-top:16px;padding:15px;background:#43d6b014;border:1px solid #43d6b04a;border-radius:7px;color:#bfd0d5;font-size:13px}.resultado strong{color:#43d6b0}.clasificacion-lista{display:grid;gap:9px}.clasificacion-fila{display:grid;grid-template-columns:45px 1fr minmax(180px,280px) 25px;align-items:center;gap:15px;padding:13px 16px;background:#193b50;border:1px solid #ffffff12;border-radius:8px}.fila-numero{color:#f2a66a;font-size:11px;font-weight:800}.clasificacion-fila strong{font-size:14px}.marca-respuesta{font-size:19px;font-weight:900}.marca-respuesta.bien{color:#43d6b0}.marca-respuesta.mal{color:#f2a66a}.nota-ayuda{font-size:11px;line-height:1.7;color:#9bb2bb;margin-top:15px}.situacion-card,.pregunta-reto{padding:20px;margin-bottom:12px;background:#193b50;border:1px solid #ffffff12;border-radius:8px}.situacion-card>p{font-size:14px;line-height:1.7;margin:10px 0 16px}.opciones-situacion,.opciones-reto{display:flex;flex-wrap:wrap;gap:9px}.opciones-situacion button,.opciones-reto button{padding:10px 13px;border:1px solid #ffffff2a;border-radius:6px;background:#102b3d;color:#dce8e9;font-size:11px;cursor:pointer;transition:.2s}.opciones-situacion button:hover,.opciones-reto button:hover,.opciones-situacion button.elegida,.opciones-reto button.elegida{border-color:#f2a66a;color:#f2a66a}.opciones-situacion button.acierto,.opciones-reto button.acierto{border-color:#43d6b0;background:#43d6b018;color:#43d6b0}.opciones-situacion button.error,.opciones-reto button.error{border-color:#f2a66a;background:#f2a66a18;color:#f2a66a}.explicacion{margin-top:14px;padding-top:12px;border-top:1px solid #ffffff17;color:#b8d0d3;font-size:12px;line-height:1.7}.pregunta-reto h3{font-size:15px;line-height:1.6;margin:10px 0 15px}.resultado-final{display:flex;align-items:center;gap:12px;flex-wrap:wrap}.resultado-final span{color:#bfd0d5}.navegacion-actividad{display:flex;justify-content:space-between;align-items:center;margin-top:28px;padding-top:20px;border-top:1px solid #ffffff19}.navegacion-actividad button{background:transparent;border:0;color:#f2a66a;font-size:10px;font-weight:900;letter-spacing:1px;cursor:pointer;padding:10px}.navegacion-actividad button:disabled{opacity:.3;cursor:not-allowed}.navegacion-actividad span{font-size:9px;letter-spacing:2px;color:#718994}.cierre-actividades{display:flex;justify-content:space-between;align-items:center;gap:25px;padding:52px 0;border-bottom:1px solid #ffffff20}.cierre-actividades h2{font-size:clamp(24px,4vw,38px);line-height:1.15;margin:10px 0 0;letter-spacing:-1.3px}.cierre-actividades button{display:flex;align-items:center;gap:20px;padding:17px 20px;background:#43d6b0;color:#10202b;border:0;border-radius:6px;font-size:9px;font-weight:900;letter-spacing:1px;cursor:pointer}.cierre-actividades button:hover{background:#70e6c7}.cierre-actividades button span{font-size:18px}.pie-pagina{display:flex;justify-content:space-between;padding-top:22px;color:#718994;font-size:9px;letter-spacing:1.5px}.pie-pagina span:first-child{color:#f2a66a;font-weight:900}
@media(max-width:900px){.ruta-grid{grid-template-columns:repeat(2,1fr)}.visual-grid{grid-template-columns:repeat(2,1fr)}}
@media(max-width:600px){.pagina-actividades{padding:0 5% 25px}.hero-actividades{padding:55px 0}.hero-dato{display:none}.hero-texto h1{letter-spacing:-2px}.ruta-grid{gap:8px}.ruta-card{min-height:140px;padding:14px}.visual-grid{grid-template-columns:1fr 1fr}.visual-imagen{height:115px}.panel-cabecera{gap:8px}.panel-simbolo{font-size:32px}.clasificacion-fila{grid-template-columns:25px 1fr 1fr 18px;gap:8px;padding:12px 8px}.clasificacion-fila strong{font-size:12px}.clasificacion-fila select{font-size:10px;padding:9px 5px}.pie-actividad{align-items:flex-start;flex-direction:column}.cierre-actividades{align-items:flex-start;flex-direction:column}.navegacion-actividad span{display:none}.pie-pagina{font-size:8px;gap:12px}}


/* AJUSTES VISUALES: títulos menta y mejor separación */
.pagina-actividades h1,
.pagina-actividades h2,
.pagina-actividades h3,
.pagina-actividades h4 {
  color: #43d6b0 !important;
}
.pagina-actividades .hero-texto h1 {
  margin: 27px 0 24px;
  line-height: 1.08;
}
.pagina-actividades .selector-cabecera h2,
.pagina-actividades .panel-cabecera h2,
.pagina-actividades .cierre-actividades h2 {
  margin-top: 13px;
  margin-bottom: 15px;
  line-height: 1.2;
}
.pagina-actividades .panel-cabecera h2 {
  margin-top: 15px;
  margin-bottom: 12px;
}
.pagina-actividades .pregunta-reto h3 {
  margin: 15px 0 19px;
  line-height: 1.65;
}

</style>
