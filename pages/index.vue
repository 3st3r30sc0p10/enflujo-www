<template>
  <div id="inicio">
    <section id="portada" ref="seccionPortada" :style="estiloPortada">
      <SvgLogo :color="general.project_color" />
      <div class="nombrePortada">
        <h1 class="titulo">{{ general.nombre }}</h1>
        <h2 class="subtitulo" :style="`background-color:${general.project_color}`">{{ general.descripcion }}</h2>
      </div>
      <canvas ref="lienzo" class="lienzo"></canvas>
    </section>

    <section v-for="(definicion, i) in general.definiciones" :key="`definicion${i}`" class="contenido">
      <h2>{{ definicion.titulo }}</h2>
      <div v-html="$md.render(definicion.contenido)"></div>
    </section>
  </div>
</template>

<script>
import { urlImagen, crearHead } from '../utilidades/ayudas';

export default {
  data() {
    return {
      estiloPortada: null,
      ctx: null,
      animReq: null,
    };
  },

  head() {
    return crearHead(this.general.nombre, null, this.general.descripcion, this.general.banner, this.$nuxt.$route.path);
  },

  computed: {
    general() {
      return this.$store.state.general.datos;
    },
  },

  beforeMount() {
    window.addEventListener('resize', this.actualizar);
    //
  },

  beforeDestroy() {
    window.removeEventListener('resize', this.actualizar);
    window.cancelAnimationFrame(this.animReq);
  },

  mounted() {
    if (!this.ctx) {
      this.crearContexto();
    }
    this.actualizar();
    this.animReq = requestAnimationFrame(this.animar);
  },

  methods: {
    actualizar() {
      // const { lienzo, seccionPortada } = this.$refs;
      // const ctx = this.ctx;
      // const dims = seccionPortada.getBoundingClientRect();
      // lienzo.width = dims.width;
      // lienzo.height = dims.height;
      // ctx.globalAlpha = 0.5;
    },

    animar() {
      // TODO: animar un dondo liquido
      // this.animReq = requestAnimationFrame(this.animar.bind(this));
    },

    crearEstiloPortada() {
      const urlImgPortada = urlImagen(this.general.public_background.id, {
        fit: 'inside',
        width: 1200,
        quality: 60,
      });

      this.estiloPortada = `background-image:url(${urlImgPortada})`;
    },

    crearContexto() {
      this.ctx = this.$refs.lienzo.getContext('2d');
      this.actualizar();
    },
  },
};
</script>

<style lang="scss" scoped>
section {
  position: relative;
  z-index: 1;
  margin: 3em 0;
}

#portada {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.nombrePortada {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.lienzo {
  position: absolute;
  top: 0;
  left: 0;
  display: inline-block;
  vertical-align: top;
  pointer-events: none;
}

.enflujoLogo {
  width: 100px;
  margin-top: 10px;
  display: block;
}

.titulo {
  font-size: 3em;
  margin: 0;
}

.subtitulo {
  font-size: 0.9em;
  color: white;
  font-weight: $fuentePrincipalPeso;
  padding: 1em;
  margin: 1em 0;
}

// Teléfonos horizontal
@media (min-width: $minCelular) {
}

// Pantallas medianas (Tablets)
@media (min-width: $minTablet) {
  #portada {
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
  }

  .enflujoLogo {
    width: 120px;
  }

  .nombrePortada {
    align-items: flex-start;
    margin-left: 30px;
  }

  .subtitulo {
    font-size: 0.85em;
  }
}

// Dispositivos grandes y pantallas medianas
@media (min-width: $minPantalla) {
}

// Pantallas grandes
@media (min-width: $minPantallaGrande) {
}
</style>
