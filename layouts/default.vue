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

/* Navigation Styling */
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

/* Containers Styling */
.container {
  min-height: calc(100vh - 3rem - (1.25rem + 3.25rem + 1rem) -200px;
  /* Berechnung: Viewport-Höhe - <Footer> - <Navigation> - <body>-Padding */
  text-align: center;
}

/* Headline Styling */
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

/* Card Styling */
.card {
  /* Default width for mobile-first */
  min-width: 100%;
  background-color: $gray-900;

  .card-title {
    font-family: "Star Wars", Arial, Helvetica, sans-serif;
  }

  .opening-crawl {
    transform-origin: 50% 100%;
    transform: perspective(250px) rotateX(20deg);
  }
}

@media (min-width: 768px) {
  /* Width for large Smartphones and higher */
  .card {
    min-width: calc(50% - 30px);
  }
}

.list-group {
  border: 1px solid transparentize($white, 0.5);
  box-shadow: 8px 8px 5px transparentize($black, 0.5);
}

.list-group-item {
  background-color: $black;
  border: none !important;
  border-bottom: 2px solid transparentize($white, 0.5) !important;

  &:last-child {
    border: none !important;
  }
}

/* Link Styling */
.nuxt-link-exact-active {
  color: $primary !important;
}

/* Transition Styling */
.page-enter-active,
.page-leave-active {
  transition: opacity 0.5s;
}

.page-enter,
.page-leave-to {
  opacity: 0;
}
</style>
