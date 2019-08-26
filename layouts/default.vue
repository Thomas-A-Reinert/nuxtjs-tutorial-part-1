<template>
  <div>
    <Navigation />
    <nuxt />
    <Footer />
  </div>
</template>

<script>
import Navigation from '~/components/Navigation'
import Footer from '~/components/Footer'

export default {
  components: {
    Navigation,
    Footer
  }
}
</script>

<style lang="SCSS">
@import '~assets/scss/bootstrap-variables.scss';
@import '~bootstrap/scss/bootstrap.scss';
@import '~bootstrap-vue/src/index.scss';

body {
  padding-top: 100px;
  padding-bottom: 100px;
  background-color: $black;
  color: $light;
}

.navbar-brand {

  #header-logo {
    max-height: 2rem;
    margin-right: 1.5rem;
  }

  h1 {
    font-family: "Star Wars", Arial, Helvetica, sans-serif;
    font-size: 1.25rem;
  }
}

.container {
  min-height: calc(100vh - 3rem - (1.25rem + 3.25rem + 1rem) -200px;
  /* Berechnung: Viewport-Höhe - <Footer> - <Navigation> - <body>-Padding */
  text-align: center;
}

.title {
  font-family: "Star Wars", Arial, Helvetica, sans-serif;
  font-weight: normal;
  font-size: 3rem;
  color: $dark;
  text-shadow:  0px 0px 3px transparentize($primary, 0.5),
                -1px 1px 3px transparentize($primary, 0.5),
                1px -1px 3px transparentize($primary, 0.5),
                -1px -1px 3px transparentize($primary, 0.5);
}

.subtitle {
  font-weight: 300;
  font-size: 2.5rem;
}

.card {
  background-color: $gray-900;

  .card-title {
    font-family: "Star Wars", Arial, Helvetica, sans-serif;
  }
}

.list-group-item {
  background-color: $black;
}

.nuxt-link-exact-active {
  color: $primary !important;
}

.page-enter-active,
.page-leave-active {
  transition: opacity 0.5s;
}

.page-enter,
.page-leave-to {
  opacity: 0;
}
</style>
