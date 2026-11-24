<script setup>
import { GraduationCap, MapPin, CalendarDays, UserRound } from 'lucide-vue-next'

const emit = defineEmits(['navigate'])
</script>

<template>
  <main class="pagina-creditos">
    <section class="creditos-contenido">
      <div class="creditos-etiqueta">
        <span class="etiqueta-linea"></span>
        MUNDO DEPORTE / CRÉDITOS
      </div>

      <h1>Detrás de <span>la experiencia.</span></h1>
      <p class="creditos-intro">
        Este Objeto Virtual de Aprendizaje fue desarrollado como un espacio
        para explorar, aprender y reconocer el valor del deporte.
      </p>

      <article class="tarjeta-autor">
        <img
          class="foto-autor"
          src="/foto-tomas-benedetti.jpeg"
          alt="Fotografía de Tomás David Benedetti Malo"
        />

        <div class="datos-autor">
          <span class="rol-autor"><UserRound :size="14" /> AUTOR</span>
          <h2>Tomás David Benedetti Malo</h2>
          <div class="dato"><GraduationCap :size="17" /> Licenciatura en Informática</div>
          <div class="dato"><MapPin :size="17" /> Universidad de Córdoba · Montería, Colombia</div>
          <div class="dato"><CalendarDays :size="17" /> 2027</div>
        </div>
      </article>

      <div class="creditos-pie">
        <span>MUNDO<span class="naranja">DEPORTE.</span></span>
        <span>APRENDER · PRACTICAR · CRECER</span>
      </div>

      <button class="volver-inicio" @click="emit('navigate', 'inicio')">
        VOLVER AL INICIO <span>↗</span>
      </button>
    </section>
  </main>
</template>

<style scoped>
.pagina-creditos {
  min-height: calc(100vh - 85px);
  display: grid;
  place-items: center;
  padding: 48px 7%;
  background:
    radial-gradient(ellipse at 82% 18%, #ed93451b, transparent 36%),
    #101820;
  color: #f4f2ed;
  font-family: 'Inter', sans-serif;
}
.creditos-contenido { width: min(760px, 100%); }
.creditos-etiqueta {
  display: flex; align-items: center; gap: 10px;
  color: #aab4bd; font-size: 9px; font-weight: 800; letter-spacing: 2px;
}
.etiqueta-linea { width: 25px; height: 2px; background: #ed9345; }
h1 {
  margin: 17px 0 9px; color: #f4f2ed;
  font-family: 'Barlow Condensed', 'Inter', sans-serif;
  font-size: clamp(38px, 5vw, 58px); line-height: 1.05;
}
h1 span { color: #edaa70; }
.creditos-intro {
  max-width: 570px; margin: 0 0 28px;
  color: #aab4bd; font-size: 13px; line-height: 1.8;
}
.tarjeta-autor {
  display: flex; align-items: center; gap: 24px;
  padding: 23px; border: 1px solid #ed93454a;
  border-radius: 15px; background: #192632;
  box-shadow: 0 18px 50px #0003;
}
.foto-autor {
  width: 112px; height: 112px; flex: 0 0 112px;
  object-fit: cover; object-position: center 35%;
  border-radius: 12px; border: 2px solid #ed9345;
}
.datos-autor { min-width: 0; }
.rol-autor {
  display: flex; align-items: center; gap: 7px;
  color: #edaa70; font-size: 9px; font-weight: 800; letter-spacing: 1.8px;
}
.datos-autor h2 {
  margin: 9px 0 13px; color: #f4f2ed;
  font-size: clamp(18px, 2.5vw, 23px); line-height: 1.2;
}
.dato {
  display: flex; align-items: center; gap: 9px;
  margin-top: 8px; color: #c0c9cf; font-size: 12px;
}
.dato :deep(svg) { color: #ed9345; flex: 0 0 auto; }
.creditos-pie {
  display: flex; justify-content: space-between; gap: 15px;
  margin-top: 24px; padding-top: 16px;
  border-top: 1px solid #ffffff20;
  color: #84919a; font-size: 8px; font-weight: 800; letter-spacing: 1.5px;
}
.creditos-pie > span:first-child { color: #f4f2ed; font-size: 11px; }
.naranja { color: #ed9345; }
.volver-inicio {
  margin-top: 24px; padding: 11px 15px;
  border: 1px solid #ed9345; border-radius: 5px;
  background: transparent; color: #edaa70;
  font-size: 9px; font-weight: 800; letter-spacing: 1px;
  cursor: pointer; transition: .2s ease;
}
.volver-inicio:hover { background: #ed9345; color: #101820; }
.volver-inicio span { margin-left: 12px; }
@media (max-width: 560px) {
  .tarjeta-autor { align-items: flex-start; gap: 15px; padding: 17px; }
  .foto-autor { width: 82px; height: 82px; flex-basis: 82px; }
  .dato { align-items: flex-start; font-size: 10px; line-height: 1.5; }
  .creditos-pie { flex-direction: column; }
}
</style>
