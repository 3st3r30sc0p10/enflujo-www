<template>
  <div id="contenedor">
    <Navegacion :colorIcono="colorIcono" />
    <Menu :menuAbierto="menuAbierto" @resolverMenu="resolverMenu" @cerrarMenu="cerrarMenu" />
    <main role="main">
      <Nuxt keepAlive />
    </main>
    <Footer />
  </div>
</template>

<script>
export default {
  data() {
    return {
      colorIcono: '#FFF',
      menuAbierto: false,
    };
  },

  computed: {
    general() {
      return this.$store.state.general.datos;
    },
  },

  methods: {
    /**
     * Intercambia el estado del menú: si esta abierto lo cierra, si esta cerrado lo abre.
     */
    resolverMenu() {
      this.menuAbierto = !this.menuAbierto;
    },

    /**
     * Cierra el menú, lo usamos en navegación si el menú esta abierto.
     */
    cerrarMenu() {
      if (this.menuAbierto) {
        this.menuAbierto = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@use "sass:color";
#contenedor {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  margin-top: $anchoMenu;
  flex-grow: 1;
  // background-color: color.scale($colorPrincipal, $lightness: 90%);
}
</style>
