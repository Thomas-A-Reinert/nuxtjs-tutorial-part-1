<template>
  <section class="container">
    <div>
      <h1 class="title">
        Star Wars Films
      </h1>
      <h2 class="subtitle text-primary">
        – A Nuxt.js project –
      </h2>
    </div>
  </section>
</template>

<script>
import _ from 'lodash'
import axios from '~/plugins/axios'

export default {
  components: {},
  data() {
    return {}
  },
  computed: {
    filmsOrderedByID: function() {
      const filmsOrdered = _.orderBy(this.films, 'episode_id')
      return filmsOrdered
    }
  },
  asyncData() {
    return axios.get('films/').then(res => ({
      films: res.data.results
    }))
  },
  /* eslint-disable */
  created() {
    console.log(_.isEmpty() ? 'Lodash is available here!' : 'Uh oh..')
  }
  /* eslint-enable */
}
</script>

<style></style>
