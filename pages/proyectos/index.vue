<template>
  <div>
    <PaginaCargando v-if="$fetchState.pending" />
    <Error v-else-if="$fetchState.error" />

    <template v-else>
      <h1>{{ pagina.titulo }}</h1>
      <p>{{ pagina.contenido }}</p>

      <div class="contenedorProyectos">
        <NuxtLink v-for="proyecto in proyectos" :key="proyecto.id" :to="`/proyectos/${proyecto.slug}`">
          {{ proyecto.titulo }}
        </NuxtLink>
      </div>
    </template>
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request';
import { crearHead } from '../../utilidades/ayudas';

export default {
  data() {
    return {
      pagina: {},
      proyectos: [],
    };
  },

  async fetch() {
    const query = gql`
      query {
        paginas(filter: { slug: { _eq: "proyectos" }, status: { _eq: "published" } }, limit: 1) {
          titulo
          slug
          descripcion
          contenido
          banner {
            id
            title
          }
        }
        proyectos(filter: { status: { _eq: "published" } }) {
          id
          titulo
          slug
          fecha_publicacion
          banner {
            id
          }
        }
      }
    `;

    const { paginas, proyectos } = await this.$graphql.principal.request(query);

    if (paginas.length && paginas[0].slug) {
      this.pagina = paginas[0];
    } else {
      if (process.server) {
        this.$nuxt.context.res.statusCode = 404;
      }
      throw new Error('La página no existe');
    }

    if (proyectos && proyectos.length) {
      this.proyectos = proyectos;
    }
  },

  head() {
    return crearHead(
      this.$store.state.general.datos.nombre,
      this.pagina.titulo,
      this.pagina.descripcion,
      this.pagina.banner,
      this.$nuxt.$route.path
    );
  },
};
</script>

<style lang="scss" scoped></style>
