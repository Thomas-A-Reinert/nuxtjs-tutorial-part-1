<template>
  <b-navbar toggleable="md" type="dark" variant="dark" fixed="top">
    <b-navbar-brand to="/" class="d-flex align-items-center">
      <img
        id="header-logo"
        src="~assets/imgs/SW_opening_crawl_logo.svg"
        alt="NUXT.JS – Star Wars Films"
      />
      <h1 class="h4">Star Wars Films</h1>
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav class="ml-auto">
        <b-nav-item to="/">
          Home
        </b-nav-item>
        <b-nav-item to="/test">
          Test
        </b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
export default {
  components: {}
}
</script>

<style></style>
