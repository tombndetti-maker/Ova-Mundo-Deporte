<script setup>
import { computed } from 'vue'

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
    descripcion: 'Reconoce qué es el deporte, cómo se diferencia de la actividad física y por qué es importante para las personas y la sociedad.'
  },
  2: { titulo: 'Tipos de deportes', descripcion: 'Conoce las diferentes formas de clasificar las disciplinas deportivas.' },
  3: { titulo: 'Beneficios del deporte', descripcion: 'Explora los aportes físicos, mentales, emocionales y sociales del deporte.' },
  4: { titulo: 'Valores deportivos', descripcion: 'Reconoce los valores que se pueden poner en práctica mediante el deporte.' },
  5: { titulo: 'Práctica deportiva responsable', descripcion: 'Conoce acciones básicas para realizar actividad deportiva de manera responsable.' }
}

const moduloActual = computed(() => modulos[props.numeroContenido] ?? modulos[1])
const esModuloUno = computed(() => props.numeroContenido === 1)
const esModuloDos = computed(() => props.numeroContenido === 2)
const numeroFormateado = computed(() => String(props.numeroContenido).padStart(2, '0'))

function irAActividades() {
  emit('navigate', `actividades-${props.numeroContenido}`)
}
</script>

<template>
  <main class="pagina-contenido">
    <section class="hero-contenido">
      <div class="hero-texto">
        <span class="sobretitulo">MUNDO DEPORTE / APRENDIZAJE</span>
        <span class="numero-modulo">MÓDULO {{ numeroFormateado }}</span>
        <h1>{{ moduloActual.titulo }}<span>.</span></h1>
        <p>{{ moduloActual.descripcion }}</p>
      </div>
      <div class="hero-sello" aria-hidden="true">
        <span>MD</span>
        <small>APRENDE<br />Y EXPLORA</small>
      </div>
    </section>

    <template v-if="esModuloUno">
      <section class="introduccion bloque">
        <div class="indice-seccion">01 / CONCEPTO</div>
        <div class="contenido-seccion">
          <h2>¿Qué es el deporte?</h2>
          <p class="texto-destacado">
            El deporte es una actividad física que se practica siguiendo reglas o normas
            determinadas y que requiere habilidades, esfuerzo y preparación.
          </p>
          <p>
            Puede realizarse de manera individual o en equipo, con fines recreativos,
            formativos o competitivos. A través de su práctica, las personas desarrollan
            capacidades físicas, aprenden a superar retos y comparten experiencias con otras.
          </p>

          <h3>Características principales</h3>
          <div class="rejilla-caracteristicas">
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">01</span>
              <h4>Reglas</h4>
              <p>Cuenta con normas que orientan la práctica y organizan la participación.</p>
            </article>
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">02</span>
              <h4>Habilidades</h4>
              <p>Requiere capacidades como coordinación, velocidad, fuerza o resistencia.</p>
            </article>
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">03</span>
              <h4>Preparación</h4>
              <p>La práctica y el entrenamiento ayudan a desarrollar y mejorar habilidades.</p>
            </article>
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">04</span>
              <h4>Objetivos</h4>
              <p>Puede practicarse para aprender, recrearse, mejorar o competir.</p>
            </article>
          </div>

          <h3>Algunos ejemplos de disciplinas deportivas</h3>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo futbol">⚽</div>
              <div class="texto-ejemplo">
                <span>DEPORTE COLECTIVO</span>
                <h4>Fútbol</h4>
                <p>Dos equipos buscan marcar goles en la portería contraria, respetando las reglas del juego.</p>
              </div>
            </article>
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo baloncesto">🏀</div>
              <div class="texto-ejemplo">
                <span>DEPORTE COLECTIVO</span>
                <h4>Baloncesto</h4>
                <p>Dos equipos intentan conseguir puntos introduciendo el balón en la canasta rival.</p>
              </div>
            </article>
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo natacion">🏊</div>
              <div class="texto-ejemplo">
                <span>DISCIPLINA ACUÁTICA</span>
                <h4>Natación</h4>
                <p>Consiste en desplazarse en el agua mediante diferentes estilos y técnicas.</p>
              </div>
            </article>
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo atletismo">🏃</div>
              <div class="texto-ejemplo">
                <span>DEPORTE INDIVIDUAL</span>
                <h4>Atletismo</h4>
                <p>Reúne pruebas como carreras, saltos y lanzamientos.</p>
              </div>
            </article>
          </div>
        </div>
      </section>

      <section class="bloque bloque-diferencias">
        <div class="indice-seccion">02 / DIFERENCIAS</div>
        <div class="contenido-seccion">
          <h2>Deporte y actividad física</h2>
          <p>
            Aunque están relacionados, los conceptos de deporte y actividad física no
            significan exactamente lo mismo.
          </p>
          <div class="comparacion">
            <article class="tarjeta-comparacion">
              <div class="comparacion-icono">🚶</div>
              <h3>Actividad física</h3>
              <p>
                Comprende los movimientos corporales que implican un gasto de energía.
                Puede estar presente en la vida cotidiana, el trabajo, los desplazamientos
                y el tiempo libre.
              </p>
              <strong>Ejemplos</strong>
              <ul>
                <li>Caminar.</li>
                <li>Subir escaleras.</li>
                <li>Bailar.</li>
                <li>Realizar tareas domésticas.</li>
              </ul>
            </article>
            <article class="tarjeta-comparacion destacada">
              <div class="comparacion-icono">🏅</div>
              <h3>Deporte</h3>
              <p>
                Es una forma de actividad física que se desarrolla como una disciplina,
                con reglas, características y objetivos definidos.
              </p>
              <strong>Ejemplos</strong>
              <ul>
                <li>Practicar fútbol.</li>
                <li>Jugar baloncesto.</li>
                <li>Competir en natación.</li>
                <li>Participar en atletismo.</li>
              </ul>
            </article>
          </div>
          <div class="idea-clave">
            <span>IDEA CLAVE</span>
            <p>Todo deporte implica actividad física, pero no toda actividad física constituye un deporte.</p>
          </div>
        </div>
      </section>

      <section class="bloque">
        <div class="indice-seccion">03 / IMPORTANCIA</div>
        <div class="contenido-seccion">
          <h2>Importancia del deporte en la sociedad</h2>
          <p>
            El deporte ocupa un lugar importante en la sociedad porque ofrece espacios
            para el aprendizaje, la recreación, la participación y el desarrollo personal.
            Su importancia no se limita a ganar competencias: también puede favorecer
            la convivencia, la integración y la formación de valores.
          </p>
          <div class="rejilla-importancia">
            <article class="tarjeta-importancia">
              <span>01</span>
              <h3>Desarrollo físico</h3>
              <p>Favorece el desarrollo de capacidades como la fuerza, la resistencia, la coordinación y la movilidad.</p>
            </article>
            <article class="tarjeta-importancia">
              <span>02</span>
              <h3>Convivencia e integración</h3>
              <p>Facilita la interacción entre personas, la cooperación y la participación en actividades compartidas.</p>
            </article>
            <article class="tarjeta-importancia">
              <span>03</span>
              <h3>Formación en valores</h3>
              <p>Ofrece oportunidades para practicar el respeto, la disciplina, la responsabilidad y el juego limpio.</p>
            </article>
            <article class="tarjeta-importancia">
              <span>04</span>
              <h3>Participación social</h3>
              <p>Promueve espacios comunitarios de recreación, encuentro y participación.</p>
            </article>
          </div>
        </div>
      </section>

      <section class="resumen-modulo">
        <div>
          <span class="sobretitulo">PARA RECORDAR</span>
          <h2>Lo esencial del módulo</h2>
        </div>
        <ul>
          <li>El deporte es una actividad física organizada mediante reglas y objetivos.</li>
          <li>Puede practicarse individualmente o en equipo.</li>
          <li>La actividad física incluye movimientos de la vida cotidiana.</li>
          <li>El deporte contribuye al desarrollo físico y a la convivencia social.</li>
        </ul>
      </section>
    </template>

    <template v-else-if="esModuloDos">
      <section class="bloque">
        <div class="indice-seccion">01 / CLASIFICACIÓN</div>
        <div class="contenido-seccion">
          <h2>¿Cómo se clasifican los deportes?</h2>
          <p class="texto-destacado">
            Los deportes pueden organizarse en diferentes tipos según la forma de participación,
            el espacio donde se practican, el propósito de la actividad y las habilidades que requieren.
          </p>
          <p>
            Conocer estas clasificaciones permite identificar qué caracteriza a cada disciplina y
            reconocer que no todos los deportes se practican de la misma manera. En este módulo
            estudiaremos cinco tipos: individuales, colectivos, de combate, acuáticos y de precisión.
          </p>
          <div class="idea-clave">
            <span>PARA TENER EN CUENTA</span>
            <p>Una disciplina puede compartir características de más de una clasificación. Por ejemplo, la natación es acuática y sus pruebas pueden ser individuales o por equipos.</p>
          </div>
        </div>
      </section>

      <section class="galeria-deportes">
        <div class="galeria-cabecera">
          <span class="sobretitulo">EXPLORA VISUALMENTE</span>
          <h2>Cinco formas de vivir el deporte</h2>
          <p>Observa algunas disciplinas representativas de cada clasificación. Pasa el cursor sobre las imágenes para descubrir sus nombres.</p>
        </div>
        <div class="galeria-grid">
          <article class="foto-deporte">
            <img src="https://images.unsplash.com/photo-1461896836934-ffe607ba8211?auto=format&fit=crop&w=900&q=85" alt="Atleta corriendo en una pista de atletismo" loading="lazy" />
            <div class="foto-etiqueta"><span>01</span><strong>Individuales</strong></div>
          </article>
          <article class="foto-deporte">
            <img src="https://images.unsplash.com/photo-1546519638-68e109498ffc?auto=format&fit=crop&w=900&q=85" alt="Partido de baloncesto" loading="lazy" />
            <div class="foto-etiqueta"><span>02</span><strong>Colectivos</strong></div>
          </article>
          <article class="foto-deporte">
            <img src="https://images.unsplash.com/photo-1549719386-74dfcbf7dbed?auto=format&fit=crop&w=900&q=85" alt="Entrenamiento de boxeo" loading="lazy" />
            <div class="foto-etiqueta"><span>03</span><strong>Combate</strong></div>
          </article>
          <article class="foto-deporte">
            <img src="https://images.unsplash.com/photo-1530549387789-4c1017266635?auto=format&fit=crop&w=900&q=85" alt="Nadador en una piscina" loading="lazy" />
            <div class="foto-etiqueta"><span>04</span><strong>Acuáticos</strong></div>
          </article>
          <article class="foto-deporte">
            <img src="https://images.unsplash.com/photo-1518604666860-9ed391f76460?auto=format&fit=crop&w=900&q=85" alt="Práctica de tiro con arco" loading="lazy" />
            <div class="foto-etiqueta"><span>05</span><strong>Precisión</strong></div>
          </article>
        </div>
        <p class="nota-galeria">Las imágenes son ilustrativas y ayudan a reconocer visualmente las distintas modalidades deportivas.</p>
      </section>

      <section class="bloque">
        <div class="indice-seccion">02 / INDIVIDUALES</div>
        <div class="contenido-seccion">
          <h2>Deportes individuales</h2>
          <p class="texto-destacado">
            Son disciplinas en las que el participante realiza la prueba o busca el resultado por
            su propio desempeño, sin depender de un equipo de compañeros durante la ejecución principal.
          </p>
          <p>
            La persona se prepara, toma decisiones y procura mejorar sus propias habilidades. En estas
            disciplinas suelen ser importantes la concentración, la constancia, la técnica y el control
            del esfuerzo. Aunque la participación sea individual, el deportista puede contar con el apoyo
            de entrenadores, compañeros y otras personas.
          </p>
          <div class="rejilla-caracteristicas">
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">01</span>
              <h4>Desempeño personal</h4>
              <p>El resultado depende principalmente de la ejecución del propio participante.</p>
            </article>
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">02</span>
              <h4>Preparación</h4>
              <p>Requiere práctica para desarrollar la técnica y mejorar las capacidades necesarias.</p>
            </article>
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">03</span>
              <h4>Concentración</h4>
              <p>El deportista debe mantener la atención y tomar decisiones durante la prueba.</p>
            </article>
            <article class="tarjeta-caracteristica">
              <span class="icono-caracteristica">04</span>
              <h4>Superación personal</h4>
              <p>Permite comparar el propio progreso y trabajar para alcanzar metas.</p>
            </article>
          </div>
          <h3>Ejemplos</h3>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo atletismo">🏃</div>
              <div class="texto-ejemplo"><span>DEPORTE INDIVIDUAL</span><h4>Atletismo</h4><p>Incluye pruebas como carreras, saltos y lanzamientos. En muchas pruebas cada atleta compite por su propio resultado.</p></div>
            </article>
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo natacion">🏊</div>
              <div class="texto-ejemplo"><span>DEPORTE ACUÁTICO</span><h4>Natación</h4><p>En las pruebas individuales, cada nadador recorre una distancia utilizando un estilo permitido y busca completar la prueba en el menor tiempo.</p></div>
            </article>
            <article class="tarjeta-ejemplo">
              <div class="imagen-ejemplo">🎾</div>
              <div class="texto-ejemplo"><span>DEPORTE INDIVIDUAL</span><h4>Tenis individual</h4><p>Dos participantes se enfrentan en una cancha y buscan ganar puntos enviando la pelota al campo contrario.</p></div>
            </article>
          </div>
        </div>
      </section>

      <section class="bloque">
        <div class="indice-seccion">03 / COLECTIVOS</div>
        <div class="contenido-seccion">
          <h2>Deportes colectivos</h2>
          <p class="texto-destacado">
            Son disciplinas en las que dos o más equipos participan y sus integrantes colaboran
            para alcanzar un objetivo común, siguiendo las reglas establecidas.
          </p>
          <p>
            En estos deportes, el resultado depende de la participación coordinada de los jugadores.
            Por eso son importantes la comunicación, la cooperación, la organización y el respeto por
            los compañeros y los adversarios. Cada integrante puede cumplir una función diferente dentro
            del equipo.
          </p>
          <div class="rejilla-caracteristicas">
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">01</span><h4>Trabajo en equipo</h4><p>Los participantes colaboran para lograr una meta compartida.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">02</span><h4>Comunicación</h4><p>Los jugadores necesitan comunicarse para coordinar sus acciones.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">03</span><h4>Funciones</h4><p>Los integrantes pueden asumir posiciones y responsabilidades distintas.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">04</span><h4>Estrategia</h4><p>El equipo organiza sus acciones de acuerdo con las reglas y situaciones del juego.</p></article>
          </div>
          <h3>Ejemplos</h3>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo futbol">⚽</div><div class="texto-ejemplo"><span>DEPORTE COLECTIVO</span><h4>Fútbol</h4><p>Dos equipos buscan marcar goles en la portería contraria. Para avanzar y defender, sus jugadores combinan pases, movimientos y estrategias.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo baloncesto">🏀</div><div class="texto-ejemplo"><span>DEPORTE COLECTIVO</span><h4>Baloncesto</h4><p>Dos equipos intentan anotar puntos introduciendo el balón en la canasta rival. Se utilizan pases, desplazamientos y lanzamientos.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🏐</div><div class="texto-ejemplo"><span>DEPORTE COLECTIVO</span><h4>Voleibol</h4><p>Dos equipos separados por una red intentan enviar el balón al suelo del campo contrario, respetando las reglas de contacto.</p></div></article>
          </div>
        </div>
      </section>

      <section class="bloque">
        <div class="indice-seccion">04 / COMBATE</div>
        <div class="contenido-seccion">
          <h2>Deportes de combate</h2>
          <p>
            Son disciplinas en las que dos participantes se enfrentan directamente bajo reglas
            específicas. Utilizan técnicas de ataque, defensa, desplazamiento y control corporal.
            Su práctica exige preparación, concentración y respeto por la integridad del oponente.
          </p>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🥋</div><div class="texto-ejemplo"><span>DEPORTE DE COMBATE</span><h4>Judo</h4><p>Disciplina en la que se emplean técnicas de agarre, equilibrio y proyección para controlar al oponente según las reglas.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🥊</div><div class="texto-ejemplo"><span>DEPORTE DE COMBATE</span><h4>Boxeo</h4><p>Dos deportistas se enfrentan utilizando golpes permitidos con los puños, dentro de un espacio y tiempo reglamentados.</p></div></article>
          </div>
          <div class="idea-clave"><span>CARACTERÍSTICA IMPORTANTE</span><p>El respeto por las reglas, el autocontrol y la seguridad de los participantes son fundamentales.</p></div>
        </div>
      </section>

      <section class="bloque">
        <div class="indice-seccion">05 / ACUÁTICOS</div>
        <div class="contenido-seccion">
          <h2>Deportes acuáticos</h2>
          <p>
            Son disciplinas deportivas que se realizan en el agua, como piscinas, ríos o espacios
            acuáticos habilitados. Según la disciplina, pueden requerir técnicas de desplazamiento,
            coordinación, resistencia y adaptación al medio acuático.
          </p>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo natacion">🏊</div><div class="texto-ejemplo"><span>DEPORTE ACUÁTICO</span><h4>Natación</h4><p>Consiste en desplazarse en el agua mediante estilos y técnicas determinadas. Puede incluir pruebas individuales y de relevos.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🤽</div><div class="texto-ejemplo"><span>DEPORTE ACUÁTICO COLECTIVO</span><h4>Waterpolo</h4><p>Deporte por equipos que se juega en una piscina. Los participantes pasan y lanzan un balón para intentar marcar goles.</p></div></article>
          </div>
        </div>
      </section>

      <section class="bloque">
        <div class="indice-seccion">06 / PRECISIÓN</div>
        <div class="contenido-seccion">
          <h2>Deportes de precisión</h2>
          <p>
            Son disciplinas en las que el objetivo principal consiste en dirigir un objeto o realizar
            una acción con exactitud para alcanzar un blanco, una zona determinada o una marca.
            Requieren concentración, coordinación, control del movimiento y práctica técnica.
          </p>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🏹</div><div class="texto-ejemplo"><span>DEPORTE DE PRECISIÓN</span><h4>Tiro con arco</h4><p>El participante utiliza un arco para lanzar flechas hacia una diana e intenta alcanzar la zona de mayor puntuación.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🎳</div><div class="texto-ejemplo"><span>DEPORTE DE PRECISIÓN</span><h4>Boliche</h4><p>El jugador hace rodar una bola por una pista para derribar el mayor número posible de pinos.</p></div></article>
          </div>
        </div>
      </section>

      <section class="resumen-modulo">
        <div><span class="sobretitulo">PARA RECORDAR</span><h2>Lo esencial del módulo</h2></div>
        <ul>
          <li>Los deportes pueden clasificarse según la forma de participación y las características de su práctica.</li>
          <li>En los deportes individuales predomina el desempeño personal.</li>
          <li>En los deportes colectivos los integrantes colaboran para alcanzar una meta común.</li>
          <li>Los deportes de combate implican enfrentamientos reglamentados entre participantes.</li>
          <li>Los deportes acuáticos se practican en el agua y los de precisión buscan exactitud en la ejecución.</li>
        </ul>
      </section>
    </template>

    <template v-else-if="numeroContenido === 3">
      <section class="bloque">
        <div class="indice-seccion">01 / BENEFICIOS FÍSICOS</div>
        <div class="contenido-seccion">
          <h2>El deporte fortalece el cuerpo</h2>
          <p class="texto-destacado">La práctica deportiva habitual contribuye al desarrollo y mantenimiento de las capacidades físicas y favorece el funcionamiento del organismo.</p>
          <p>Al realizar una actividad deportiva, el cuerpo se mueve y trabaja de distintas maneras. Dependiendo de la disciplina y de la intensidad, pueden participar la fuerza, la resistencia, la velocidad, la flexibilidad, el equilibrio y la coordinación. La práctica debe adaptarse a las condiciones y posibilidades de cada persona.</p>
          <div class="rejilla-caracteristicas">
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">01</span><h4>Condición física</h4><p>Ayuda a desarrollar la resistencia y la capacidad para realizar esfuerzos de manera progresiva.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">02</span><h4>Fuerza y movilidad</h4><p>Permite trabajar los músculos, la movilidad de las articulaciones y el control del cuerpo.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">03</span><h4>Coordinación</h4><p>Favorece la organización de los movimientos y la relación entre percepción y acción.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">04</span><h4>Bienestar corporal</h4><p>Cuando se practica de forma adecuada, contribuye al cuidado general de la salud.</p></article>
          </div>
        </div>
      </section>
      <section class="galeria-deportes">
        <div class="galeria-cabecera"><span class="sobretitulo">EL CUERPO EN MOVIMIENTO</span><h2>Movimiento y bienestar</h2><p>Distintas disciplinas permiten trabajar capacidades físicas diferentes. La variedad de movimientos hace parte de la riqueza de la práctica deportiva.</p></div>
        <div class="galeria-grid">
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1538805060514-97d9cc17730c?auto=format&fit=crop&w=900&q=85" alt="Persona corriendo al aire libre" loading="lazy"><div class="foto-etiqueta"><span>01</span><strong>Resistencia</strong></div></article>
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1581009146145-b5ef050c2e1e?auto=format&fit=crop&w=900&q=85" alt="Entrenamiento de fuerza" loading="lazy"><div class="foto-etiqueta"><span>02</span><strong>Fuerza</strong></div></article>
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1518611012118-696072aa579a?auto=format&fit=crop&w=900&q=85" alt="Persona realizando estiramientos" loading="lazy"><div class="foto-etiqueta"><span>03</span><strong>Flexibilidad</strong></div></article>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">02 / BIENESTAR MENTAL Y EMOCIONAL</div>
        <div class="contenido-seccion">
          <h2>También beneficia la mente y las emociones</h2>
          <p>El deporte no involucra únicamente el movimiento corporal. Durante la práctica, las personas pueden experimentar satisfacción, motivación y confianza al aprender habilidades, superar retos y reconocer sus avances.</p>
          <div class="rejilla-caracteristicas">
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">A</span><h4>Manejo de emociones</h4><p>Ofrece oportunidades para reconocer emociones que aparecen al ganar, perder, esforzarse o enfrentar dificultades.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">B</span><h4>Confianza personal</h4><p>Al practicar y observar progresos, la persona puede fortalecer la percepción de sus propias capacidades.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">C</span><h4>Concentración</h4><p>Muchas disciplinas requieren mantener la atención, seguir instrucciones y tomar decisiones.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">D</span><h4>Constancia</h4><p>La práctica permite establecer metas y trabajar de manera gradual para alcanzarlas.</p></article>
          </div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">03 / BENEFICIOS SOCIALES</div>
        <div class="contenido-seccion">
          <h2>El deporte nos conecta</h2>
          <p>Los espacios deportivos reúnen a personas con diferentes experiencias e intereses. Al compartir una actividad, se crean oportunidades para comunicarse, cooperar, respetar acuerdos y construir relaciones.</p>
          <div class="rejilla-ejemplos">
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🤝</div><div class="texto-ejemplo"><span>CONVIVENCIA</span><h4>Relaciones sociales</h4><p>La práctica compartida facilita el encuentro, la comunicación y el respeto entre participantes.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🧩</div><div class="texto-ejemplo"><span>COOPERACIÓN</span><h4>Trabajo conjunto</h4><p>En actividades grupales se aprende a coordinar esfuerzos y aportar a una meta común.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🌍</div><div class="texto-ejemplo"><span>INTEGRACIÓN</span><h4>Participación</h4><p>El deporte puede crear espacios de encuentro para personas de distintas edades y comunidades.</p></div></article>
            <article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🗣️</div><div class="texto-ejemplo"><span>COMUNICACIÓN</span><h4>Diálogo</h4><p>Compartir reglas, decisiones y experiencias ayuda a practicar una comunicación respetuosa.</p></div></article>
          </div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">04 / HÁBITOS SALUDABLES</div>
        <div class="contenido-seccion">
          <h2>El deporte como parte de una vida saludable</h2>
          <p>Los beneficios se relacionan con la manera en que organizamos nuestra vida cotidiana. La actividad deportiva puede acompañarse de hábitos que favorecen el bienestar, como alimentarse de forma equilibrada, hidratarse, descansar y mantener una rutina de movimiento adecuada.</p>
          <div class="rejilla-caracteristicas">
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">01</span><h4>Alimentación equilibrada</h4><p>Aportar al cuerpo alimentos variados ayuda a cubrir sus necesidades de energía y nutrientes.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">02</span><h4>Hidratación</h4><p>Beber agua durante el día y según las necesidades de la actividad ayuda a reponer líquidos.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">03</span><h4>Descanso</h4><p>El sueño y las pausas permiten recuperarse del esfuerzo y mantener el bienestar.</p></article>
            <article class="tarjeta-caracteristica"><span class="icono-caracteristica">04</span><h4>Regularidad</h4><p>Mantener una rutina realista y progresiva facilita incorporar el movimiento a la vida diaria.</p></article>
          </div>
          <div class="idea-clave"><span>IDEA CLAVE</span><p>Los beneficios dependen de una práctica regular, adecuada a cada persona y acompañada de hábitos saludables.</p></div>
        </div>
      </section>
      <section class="resumen-modulo"><div><span class="sobretitulo">PARA RECORDAR</span><h2>Lo esencial del módulo</h2></div><ul><li>El deporte puede contribuir al desarrollo de capacidades físicas como fuerza, resistencia y coordinación.</li><li>La práctica también ofrece oportunidades para trabajar la concentración, la confianza y el manejo de emociones.</li><li>Compartir actividades deportivas puede fortalecer la convivencia, la comunicación y la cooperación.</li><li>La alimentación equilibrada, la hidratación, el descanso y la regularidad complementan una vida activa.</li></ul></section>
    </template>

    <template v-else-if="numeroContenido === 4">
      <section class="bloque">
        <div class="indice-seccion">01 / EL DEPORTE Y LOS VALORES</div>
        <div class="contenido-seccion">
          <h2>Más que competir: aprender a convivir</h2>
          <p class="texto-destacado">El deporte es un espacio en el que se ponen en práctica decisiones y comportamientos que influyen en la relación con los demás.</p>
          <p>Durante un entrenamiento o una competencia, las personas siguen reglas, comparten espacios, colaboran y enfrentan resultados. Estas experiencias pueden ayudar a desarrollar valores, siempre que se promuevan mediante acciones concretas y no se den por aprendidos automáticamente.</p>
          <div class="idea-clave"><span>PARA TENER EN CUENTA</span><p>Los valores deportivos se demuestran en la manera de actuar antes, durante y después de participar.</p></div>
        </div>
      </section>
      <section class="galeria-deportes">
        <div class="galeria-cabecera"><span class="sobretitulo">VALORES EN ACCIÓN</span><h2>El juego también enseña</h2><p>La convivencia deportiva se construye con actitudes visibles: escuchar, colaborar, cumplir acuerdos y reconocer a los demás.</p></div>
        <div class="galeria-grid">
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1521412644187-c49fa049e84d?auto=format&fit=crop&w=900&q=85" alt="Deportistas compartiendo en una cancha" loading="lazy"><div class="foto-etiqueta"><span>01</span><strong>Respeto</strong></div></article>
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1517649763962-0c623066013b?auto=format&fit=crop&w=900&q=85" alt="Ciclistas entrenando juntos" loading="lazy"><div class="foto-etiqueta"><span>02</span><strong>Disciplina</strong></div></article>
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1518611012118-696072aa579a?auto=format&fit=crop&w=900&q=85" alt="Personas entrenando y apoyándose" loading="lazy"><div class="foto-etiqueta"><span>03</span><strong>Compromiso</strong></div></article>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">02 / RESPETO</div>
        <div class="contenido-seccion">
          <h2>Respetar a todas las personas</h2>
          <p>El respeto consiste en reconocer la dignidad de los demás y tratar a cada participante de manera adecuada, sin importar su nivel, experiencia, equipo o resultado.</p>
          <div class="rejilla-caracteristicas"><article class="tarjeta-caracteristica"><span class="icono-caracteristica">✓</span><h4>Respetar las reglas</h4><p>Aceptar las normas que organizan la disciplina y las decisiones tomadas de acuerdo con ellas.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">✓</span><h4>Valorar al rival</h4><p>Reconocer que los demás participan y merecen un trato digno.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">✓</span><h4>Escuchar</h4><p>Atender las indicaciones de compañeros, entrenadores y árbitros.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">✓</span><h4>Evitar agresiones</h4><p>Rechazar insultos, burlas y acciones que puedan perjudicar a otras personas.</p></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">03 / DISCIPLINA</div>
        <div class="contenido-seccion">
          <h2>Ser constante y comprometido</h2>
          <p>La disciplina deportiva implica asumir con responsabilidad los compromisos de la práctica, respetar los horarios y trabajar de manera constante para mejorar. No significa exigirse sin límites: también implica reconocer cuándo es necesario descansar y cuidar el cuerpo.</p>
          <div class="rejilla-ejemplos"><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">📅</div><div class="texto-ejemplo"><span>CONSTANCIA</span><h4>Prepararse</h4><p>Asistir a las sesiones acordadas y practicar de forma organizada.</p></div></article><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🎯</div><div class="texto-ejemplo"><span>ESFUERZO</span><h4>Trabajar por metas</h4><p>Establecer objetivos posibles y avanzar progresivamente.</p></div></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">04 / TRABAJO EN EQUIPO</div>
        <div class="contenido-seccion">
          <h2>Cooperar para alcanzar objetivos</h2>
          <p>El trabajo en equipo consiste en aportar las propias capacidades y coordinarse con otras personas para conseguir un propósito compartido. Requiere comunicación, confianza y disposición para apoyar a los compañeros.</p>
          <div class="rejilla-caracteristicas"><article class="tarjeta-caracteristica"><span class="icono-caracteristica">01</span><h4>Colaboración</h4><p>Cada integrante aporta según sus posibilidades y funciones.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">02</span><h4>Comunicación</h4><p>Compartir información ayuda a organizar las acciones.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">03</span><h4>Apoyo mutuo</h4><p>Los participantes se acompañan y reconocen los aportes de los demás.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">04</span><h4>Meta común</h4><p>Las decisiones buscan contribuir al objetivo del grupo.</p></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">05 / RESPONSABILIDAD Y FAIR PLAY</div>
        <div class="contenido-seccion">
          <h2>Responsabilidad y juego limpio</h2>
          <p>La responsabilidad implica reconocer las consecuencias de las propias acciones, cuidar los espacios y materiales, cumplir los compromisos y actuar de manera segura.</p>
          <p><strong>Fair Play</strong>, o juego limpio, es una forma de participar que prioriza la honestidad, el respeto por las reglas, la consideración por los demás y la aceptación del resultado sin recurrir al engaño o a la violencia.</p>
          <div class="comparacion"><article class="tarjeta-comparacion destacada"><div class="comparacion-icono">🤝</div><h3>Juego limpio</h3><ul><li>Respetar las reglas.</li><li>Reconocer los logros de otros.</li><li>Aceptar decisiones y resultados.</li><li>Competir con honestidad.</li></ul></article><article class="tarjeta-comparacion"><div class="comparacion-icono">⚠️</div><h3>Conductas contrarias</h3><ul><li>Hacer trampa para obtener ventaja.</li><li>Agredir o intimidar.</li><li>Despreciar a otros participantes.</li><li>Ignorar deliberadamente las reglas.</li></ul></article></div>
        </div>
      </section>
      <section class="resumen-modulo"><div><span class="sobretitulo">PARA RECORDAR</span><h2>Lo esencial del módulo</h2></div><ul><li>Los valores se expresan mediante comportamientos concretos durante la práctica deportiva.</li><li>El respeto reconoce a compañeros, rivales, árbitros y reglas.</li><li>La disciplina se relaciona con la constancia y el compromiso, sin descuidar el descanso.</li><li>El trabajo en equipo requiere cooperación y comunicación.</li><li>La responsabilidad y el Fair Play promueven una participación honesta y segura.</li></ul></section>
    </template>

    <template v-else-if="numeroContenido === 5">
      <section class="bloque">
        <div class="indice-seccion">01 / CUIDAR EL CUERPO</div>
        <div class="contenido-seccion">
          <h2>Practicar deporte de manera responsable</h2>
          <p class="texto-destacado">Una práctica deportiva responsable busca disfrutar del movimiento, desarrollar habilidades y cuidar la salud, teniendo en cuenta las condiciones de cada persona y del entorno.</p>
          <p>Antes de comenzar una actividad es importante conocer sus características, utilizar los elementos apropiados y preparar el cuerpo. Durante la práctica se deben respetar las indicaciones, prestar atención a las señales corporales y evitar acciones que pongan en riesgo a uno mismo o a los demás.</p>
          <div class="idea-clave"><span>PRINCIPIO FUNDAMENTAL</span><p>La seguridad y el bienestar son más importantes que realizar una actividad a cualquier costo.</p></div>
        </div>
      </section>
      <section class="galeria-deportes">
        <div class="galeria-cabecera"><span class="sobretitulo">ANTES, DURANTE Y DESPUÉS</span><h2>Una práctica bien preparada</h2><p>La responsabilidad acompaña todo el proceso: preparación, actividad, recuperación y cuidado del material.</p></div>
        <div class="galeria-grid">
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1552674605-db6ffd4facb5?auto=format&fit=crop&w=900&q=85" alt="Persona realizando calentamiento antes de correr" loading="lazy"><div class="foto-etiqueta"><span>01</span><strong>Preparación</strong></div></article>
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1526401485004-2aa7f3b6d4b7?auto=format&fit=crop&w=900&q=85" alt="Botella de agua para hidratación" loading="lazy"><div class="foto-etiqueta"><span>02</span><strong>Hidratación</strong></div></article>
          <article class="foto-deporte"><img src="https://images.unsplash.com/photo-1517836357463-d25dfeac3438?auto=format&fit=crop&w=900&q=85" alt="Entrenamiento físico en un gimnasio" loading="lazy"><div class="foto-etiqueta"><span>03</span><strong>Práctica segura</strong></div></article>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">02 / CALENTAMIENTO</div>
        <div class="contenido-seccion">
          <h2>Preparar el cuerpo antes de comenzar</h2>
          <p>El calentamiento es una preparación previa a la actividad física o deportiva. Incluye movimientos progresivos que permiten pasar del reposo a una actividad de mayor intensidad y preparar los músculos y las articulaciones para las acciones que se realizarán.</p>
          <div class="rejilla-caracteristicas"><article class="tarjeta-caracteristica"><span class="icono-caracteristica">01</span><h4>Inicio progresivo</h4><p>Comenzar con movimientos suaves y aumentar gradualmente la actividad.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">02</span><h4>Movilidad</h4><p>Realizar movimientos controlados de las articulaciones que participarán en la actividad.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">03</span><h4>Activación</h4><p>Incluir acciones relacionadas con la disciplina que se va a practicar.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">04</span><h4>Adaptación</h4><p>Ajustar el calentamiento al tipo de actividad, la edad y las condiciones personales.</p></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">03 / HIDRATACIÓN</div>
        <div class="contenido-seccion">
          <h2>Mantener una hidratación adecuada</h2>
          <p>Durante el movimiento, el cuerpo pierde agua, especialmente cuando hace calor o el esfuerzo es prolongado. Beber agua antes, durante y después de la práctica, de acuerdo con la duración de la actividad y las necesidades personales, ayuda a reponer los líquidos perdidos.</p>
          <div class="rejilla-ejemplos"><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">💧</div><div class="texto-ejemplo"><span>ANTES</span><h4>Comenzar hidratado</h4><p>Incluir agua en la rutina diaria y evitar iniciar la actividad con sed intensa.</p></div></article><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🚰</div><div class="texto-ejemplo"><span>DURANTE</span><h4>Hacer pausas</h4><p>Disponer de agua y beber en los momentos adecuados, especialmente en actividades prolongadas o con calor.</p></div></article><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🥤</div><div class="texto-ejemplo"><span>DESPUÉS</span><h4>Recuperar líquidos</h4><p>Continuar hidratándose después del esfuerzo para reponer los líquidos perdidos.</p></div></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">04 / IMPLEMENTOS</div>
        <div class="contenido-seccion">
          <h2>Usar correctamente los implementos deportivos</h2>
          <p>Los implementos son los objetos, prendas y equipos que se utilizan para practicar una disciplina. Deben ser adecuados para la actividad, encontrarse en buen estado y utilizarse siguiendo las indicaciones correspondientes.</p>
          <div class="rejilla-caracteristicas"><article class="tarjeta-caracteristica"><span class="icono-caracteristica">👟</span><h4>Calzado apropiado</h4><p>Elegir un calzado que corresponda al terreno y al tipo de movimiento.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">🪖</span><h4>Protección</h4><p>Utilizar cascos, protectores u otros elementos cuando la disciplina lo requiera.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">🏀</span><h4>Material adecuado</h4><p>Comprobar que balones, raquetas y demás implementos sean apropiados y estén en condiciones seguras.</p></article><article class="tarjeta-caracteristica"><span class="icono-caracteristica">🧼</span><h4>Cuidado del equipo</h4><p>Limpiar, guardar y revisar los materiales después de utilizarlos.</p></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">05 / PREVENCIÓN DE LESIONES</div>
        <div class="contenido-seccion">
          <h2>Reconocer riesgos y actuar con cuidado</h2>
          <p>La prevención de lesiones reúne medidas para reducir situaciones que puedan causar daño durante la práctica. Es importante respetar la técnica, utilizar el equipo adecuado, seguir las instrucciones y aumentar la intensidad de manera gradual.</p>
          <div class="rejilla-ejemplos"><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">📈</div><div class="texto-ejemplo"><span>PROGRESIÓN</span><h4>Evitar excesos</h4><p>No aumentar bruscamente la duración, frecuencia o intensidad del entrenamiento.</p></div></article><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🧑‍🏫</div><div class="texto-ejemplo"><span>ORIENTACIÓN</span><h4>Seguir indicaciones</h4><p>Practicar con orientación adecuada y respetar las reglas de seguridad.</p></div></article><article class="tarjeta-ejemplo"><div class="imagen-ejemplo">🛑</div><div class="texto-ejemplo"><span>SEÑALES DEL CUERPO</span><h4>Detenerse si es necesario</h4><p>No ignorar el dolor, el mareo o el malestar; detener la actividad y buscar ayuda de una persona responsable.</p></div></article></div>
        </div>
      </section>
      <section class="bloque">
        <div class="indice-seccion">06 / DESCANSO</div>
        <div class="contenido-seccion">
          <h2>La recuperación también es parte del entrenamiento</h2>
          <p>El descanso permite que el cuerpo se recupere del esfuerzo. Dormir lo suficiente, alternar actividad y pausas, y evitar entrenar intensamente sin recuperación ayuda a mantener una práctica equilibrada.</p>
          <div class="idea-clave"><span>RECUERDA</span><p>Descansar no es perder el tiempo: es una parte necesaria del cuidado corporal y de una práctica deportiva responsable.</p></div>
        </div>
      </section>
      <section class="resumen-modulo"><div><span class="sobretitulo">PARA RECORDAR</span><h2>Lo esencial del módulo</h2></div><ul><li>El calentamiento prepara progresivamente el cuerpo para la actividad.</li><li>La hidratación debe acompañar la práctica según las necesidades personales y las condiciones del entorno.</li><li>Los implementos deben ser adecuados, estar en buen estado y utilizarse correctamente.</li><li>La progresión, la técnica y la atención a las señales del cuerpo ayudan a prevenir lesiones.</li><li>El descanso y la recuperación son esenciales para mantener el bienestar.</li></ul></section>
    </template>

    <footer class="pie-contenido">
      <button class="boton-secundario" @click="emit('navigate', 'inicio')">← VOLVER A INICIO</button>
      <button class="boton-principal" @click="irAActividades">IR A ACTIVIDADES <span>↗</span></button>
    </footer>
  </main>
</template>

<style scoped>
.pagina-contenido {
  --fondo: #101e2b;
  --panel: #193b50;
  --menta: #43d6b0;
  --azul: #5bafcb;
  --naranja-suave: #f2a66a;
  --blanco: #f4f8f7;
  --texto: #bfd0d5;
  min-height: calc(100vh - 80px);
  padding: clamp(35px, 6vw, 82px) 8%;
  color: var(--blanco);
  background: var(--fondo);
  font-family: 'Inter', sans-serif;
}
.hero-contenido {
  display: flex;
  align-items: end;
  justify-content: space-between;
  gap: 30px;
  padding-bottom: 48px;
  border-bottom: 1px solid #ffffff24;
}
.hero-texto { max-width: 850px; }
.sobretitulo, .numero-modulo, .indice-seccion {
  color: var(--menta);
  font-size: 10px;
  font-weight: 800;
  letter-spacing: 2px;
}
.numero-modulo { display: block; margin-top: 24px; color: var(--azul); }
.hero-contenido h1 {
  color: var(--naranja-suave);
  max-width: 850px;
  margin: 12px 0 16px;
  font-family: 'Barlow Condensed', 'Arial Narrow', sans-serif;
  font-size: clamp(48px, 7vw, 88px);
  line-height: .98;
  text-transform: uppercase;
  letter-spacing: -1px;
}
.hero-contenido h1 span { color: var(--menta); }
.hero-contenido p, .contenido-seccion > p {
  max-width: 780px;
  color: var(--texto);
  font-size: 15px;
  line-height: 1.85;
}
.hero-sello {
  flex: 0 0 130px;
  height: 130px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid #43d6b080;
  border-radius: 50%;
  color: var(--menta);
  transform: rotate(-10deg);
}
.hero-sello span { font-family: 'Barlow Condensed', sans-serif; font-size: 42px; font-weight: 900; }
.hero-sello small { font-size: 8px; line-height: 1.5; letter-spacing: 1.5px; text-align: center; }
.bloque {
  display: grid;
  grid-template-columns: 155px minmax(0, 1fr);
  gap: 30px;
  padding: 55px 0;
  border-bottom: 1px solid #ffffff20;
}
.indice-seccion { padding-top: 9px; color: var(--azul); }
.contenido-seccion h2, .contenido-seccion h3, .contenido-seccion h4, .resumen-modulo h2, .modulo-pendiente h2 {
  color: var(--naranja-suave);
}
.contenido-seccion h2, .resumen-modulo h2 {
  margin: 0 0 20px;
  font-family: 'Barlow Condensed', 'Arial Narrow', sans-serif;
  font-size: clamp(34px, 4vw, 48px);
  text-transform: uppercase;
}
.contenido-seccion h3 { margin: 35px 0 18px; font-size: 18px; }
.contenido-seccion h4 { margin: 8px 0; font-size: 18px; }
.contenido-seccion p { color: var(--texto); line-height: 1.8; font-size: 14px; }
.texto-destacado { color: var(--blanco) !important; font-size: 18px !important; line-height: 1.7 !important; }
.rejilla-caracteristicas, .rejilla-ejemplos, .rejilla-importancia {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 14px;
  margin-top: 22px;
}
.tarjeta-caracteristica, .tarjeta-ejemplo, .tarjeta-importancia, .tarjeta-comparacion {
  overflow: hidden;
  background: #193b50;
  border: 1px solid #ffffff20;
  border-radius: 12px;
}
.tarjeta-caracteristica, .tarjeta-importancia { padding: 22px; }
.icono-caracteristica, .tarjeta-importancia > span { color: var(--menta); font-family: 'Barlow Condensed', sans-serif; font-size: 28px; font-weight: 800; }
.tarjeta-caracteristica p, .tarjeta-importancia p { margin-bottom: 0; font-size: 13px; }
.tarjeta-ejemplo { display: grid; grid-template-columns: 105px minmax(0, 1fr); min-height: 150px; }
.imagen-ejemplo { display: grid; place-items: center; font-size: 45px; background: #244d61; }
.texto-ejemplo { padding: 17px; }
.texto-ejemplo > span { color: var(--menta); font-size: 8px; font-weight: 800; letter-spacing: 1px; }
.texto-ejemplo p { margin: 0; font-size: 12px; line-height: 1.6; }
.comparacion { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 16px; margin-top: 25px; }
.tarjeta-comparacion { padding: 25px; }
.tarjeta-comparacion.destacada { border-color: #43d6b080; }
.comparacion-icono { font-size: 32px; }
.tarjeta-comparacion h3 { margin: 12px 0; color: var(--naranja-suave); }
.tarjeta-comparacion p, .tarjeta-comparacion li { font-size: 13px; line-height: 1.7; color: var(--texto); }
.tarjeta-comparacion strong { color: var(--menta); font-size: 12px; }
.tarjeta-comparacion ul { padding-left: 18px; }
.idea-clave { margin-top: 20px; padding: 20px 24px; background: #43d6b014; border-left: 3px solid var(--menta); }
.idea-clave span { color: var(--menta); font-size: 9px; font-weight: 900; letter-spacing: 2px; }
.idea-clave p { margin: 8px 0 0; color: var(--blanco); font-size: 16px; font-weight: 700; }
.tarjeta-importancia { min-height: 170px; }
.resumen-modulo { display: grid; grid-template-columns: .8fr 1.2fr; gap: 35px; margin-top: 48px; padding: 30px; background: #193b50; border: 1px solid #43d6b055; border-radius: 14px; }
.resumen-modulo h2 { margin-top: 10px; margin-bottom: 0; font-size: 34px; }
.resumen-modulo ul { margin: 0; padding-left: 20px; color: var(--texto); }
.resumen-modulo li { margin: 9px 0; font-size: 13px; line-height: 1.6; }
.modulo-pendiente { margin: 55px 0; padding: 50px; text-align: center; background: #193b50; border: 1px solid #ffffff20; border-radius: 14px; }
.numero-grande { color: var(--menta); font-family: 'Barlow Condensed', sans-serif; font-size: 80px; font-weight: 900; }
.modulo-pendiente p { color: var(--texto); }
.pie-contenido { display: flex; justify-content: space-between; align-items: center; gap: 15px; padding-top: 35px; }
.boton-principal, .boton-secundario { min-height: 46px; padding: 0 20px; border-radius: 7px; font-size: 10px; font-weight: 900; letter-spacing: 1px; cursor: pointer; transition: .2s ease; }
.boton-principal { display: inline-flex; align-items: center; gap: 20px; color: #102b30; background: var(--menta); border: 1px solid var(--menta); }
.boton-principal:hover { color: var(--menta); background: transparent; }
.boton-secundario { color: var(--texto); background: transparent; border: 1px solid #ffffff35; }
.boton-secundario:hover { color: var(--menta); border-color: var(--menta); }
@media (max-width: 760px) {
  .hero-sello { display: none; }
  .bloque { grid-template-columns: 1fr; gap: 12px; padding: 38px 0; }
  .rejilla-caracteristicas, .rejilla-ejemplos, .rejilla-importancia, .comparacion, .resumen-modulo { grid-template-columns: 1fr; }
  .tarjeta-ejemplo { grid-template-columns: 85px minmax(0, 1fr); }
  .pie-contenido { align-items: stretch; flex-direction: column; }
  .boton-principal, .boton-secundario { justify-content: center; }
}
@media (max-width: 430px) {
  .pagina-contenido { padding-right: 6%; padding-left: 6%; }
  .tarjeta-ejemplo { grid-template-columns: 1fr; }
  .imagen-ejemplo { min-height: 95px; }
  .modulo-pendiente { padding: 30px 18px; }
}

.galeria-deportes {
  margin: 42px 0 12px;
  padding: clamp(20px, 3vw, 34px);
  background: linear-gradient(135deg, #193b50, #142d3d);
  border: 1px solid #43d6b055;
  border-radius: 16px;
}
.galeria-cabecera { max-width: 720px; margin-bottom: 22px; }
.galeria-cabecera h2 {
  margin: 10px 0;
  color: var(--naranja-suave);
  font-family: 'Barlow Condensed', 'Arial Narrow', sans-serif;
  font-size: clamp(30px, 4vw, 44px);
  text-transform: uppercase;
}
.galeria-cabecera p, .nota-galeria { color: var(--texto); font-size: 13px; line-height: 1.7; }
.galeria-grid { display: grid; grid-template-columns: repeat(6, minmax(0, 1fr)); gap: 12px; }
.foto-deporte {
  position: relative;
  grid-column: span 2;
  min-height: 190px;
  overflow: hidden;
  border: 1px solid #ffffff30;
  border-radius: 11px;
  background: #102b3a;
  isolation: isolate;
}
.foto-deporte:nth-child(4), .foto-deporte:nth-child(5) { grid-column: span 3; min-height: 215px; }
.foto-deporte::after {
  content: '';
  position: absolute;
  inset: 35% 0 0;
  z-index: 1;
  background: linear-gradient(transparent, #071722eF);
}
.foto-deporte img { width: 100%; height: 100%; min-height: inherit; position: absolute; inset: 0; object-fit: cover; transition: transform .55s ease, filter .4s ease; }
.foto-deporte:hover img { transform: scale(1.08); filter: saturate(1.15); }
.foto-etiqueta { position: absolute; z-index: 2; left: 16px; right: 14px; bottom: 14px; display: flex; align-items: center; gap: 10px; }
.foto-etiqueta span { color: var(--menta); font-family: 'Barlow Condensed', sans-serif; font-size: 25px; font-weight: 800; }
.foto-etiqueta strong { color: #fff; font-size: 16px; letter-spacing: .4px; }
.nota-galeria { margin: 15px 0 0; font-size: 11px; }
@media (max-width: 700px) {
  .galeria-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .foto-deporte, .foto-deporte:nth-child(4), .foto-deporte:nth-child(5) { grid-column: span 1; min-height: 165px; }
  .foto-deporte:last-child { grid-column: span 2; }
}



/* AJUSTES VISUALES: títulos menta y mejor separación */
.pagina-contenido h1,
.pagina-contenido h2,
.pagina-contenido h3,
.pagina-contenido h4 {
  color: #43d6b0 !important;
}
.pagina-contenido .hero-contenido h1 {
  margin: 20px 0 24px;
  line-height: 1.08;
}
.pagina-contenido .contenido-seccion h2,
.pagina-contenido .resumen-modulo h2,
.pagina-contenido .galeria-cabecera h2 {
  margin-top: 8px;
  margin-bottom: 25px;
  line-height: 1.2;
}
.pagina-contenido .contenido-seccion h3 {
  margin-top: 42px;
  margin-bottom: 21px;
  line-height: 1.3;
}
.pagina-contenido .contenido-seccion h4 {
  margin-top: 13px;
  margin-bottom: 11px;
  line-height: 1.3;
}
.pagina-contenido .galeria-cabecera h2 {
  margin-top: 15px;
  margin-bottom: 17px;
}
.pagina-contenido .bloque {
  margin-bottom: 22px;
}

</style>
