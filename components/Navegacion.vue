<template>
  <nav class="navegacion">
    <NuxtLink to="/" class="logoBtn">
      <SvgIcono :color="colorIcono" :fondo="colorFondo" />
    </NuxtLink>

    <NuxtLink v-for="pagina in paginas" :key="pagina.slug" :to="`/${pagina.slug}`" class="navBtn">
      {{ pagina.titulo }}
    </NuxtLink>
  </nav>
</template>

<script>
export default {
  props: {
    colorIcono: {
      type: String,
      default: '#FFF',
    },

    colorFondo: {
      type: String,
      default: '#5757f7',
    },
  },

  computed: {
    paginas() {
      return this.$store.state.general.menus.navegacion;
    },
  },
};
</script>

<style lang="scss" scoped>
a,
a:link {
  color: black;

  &:hover {
    color: $colorPrincipal;
  }
}

.navegacion {
  display: none;
  z-index: 999;
}

.enflujoIcono {
  width: $anchoMenu;
  height: $anchoMenu;
  padding: 12px;
}

.logoBtn {
  line-height: 0;
  margin-right: 10px;
}

// Teléfonos horizontal
@media (min-width: $minCelular) {
}

// Pantallas medianas (Tablets)
@media (min-width: $minTablet) {
  .navegacion {
    font-weight: $fuentePrincipalBold;
    position: fixed;
    display: flex;
    align-items: center;
    flex-direction: row;
    background-color: rgba(255, 255, 255, 0.7);
  }

  .navBtn {
    border-bottom: 1px solid transparent;
    padding: 0 0.5em 0.3em 0;
    margin-right: 0.5em;

    &.nuxt-link-active {
      border-bottom: 1px solid $colorPrincipal;
    }
  }
}

// Dispositivos grandes y pantallas medianas
@media (min-width: $minPantalla) {
}

// Pantallas grandes
@media (min-width: $minPantallaGrande) {
}
</style>
