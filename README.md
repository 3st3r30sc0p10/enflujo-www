# Sitio principal del Laboratorio EnFlujo

![CI workflow](https://github.com/enflujo/enflujo-www/actions/workflows/ci.yml/badge.svg)
![Despliegue](https://github.com/enflujo/enflujo-www/actions/workflows/despliegue.yml/badge.svg)

Creado con [Nuxt.js](https://nuxtjs.org) (Vue con _Server-Side-Rendering_)

## Instalación

```bash
# Instalar dependencias
yarn install
```

## Desarrollo local

```bash
yarn dev
```

Inicia un servidor local (con hot-reloading) en [localhost:3000](http://localhost:3000)

## Construir para producción

```bash
# Exportar app
yarn build

# Iniciar en modo de producción
yarn start
```

## Aplicar reglas de estilo al código

Para ver los errores de estilo:

```bash
yarn lint
```

**¡IMPORTANTE!** - Antes de hacer push o PR, aplicar las reglas al código:

```bash
yarn lint:fix
```

## Saltarse los procesos de Github Actions

En el mensaje del push incluir `[skip ci]`. [Explicación](https://github.blog/changelog/2021-02-08-github-actions-skip-pull-request-and-push-workflows-with-skip-ci/)
