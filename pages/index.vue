<template>
  <section class="container">
    <div>
      <h1 class="title">
        Star Wars Films
      </h1>
      <h2 class="subtitle text-primary mb-5">
        – A Nuxt.js project –
      </h2>
    </div>
    <div class="sorting mb-3">
      <h3>Sort by:</h3>
      <b-button-group>
        <b-button @click="sort('episode_id')">Episode</b-button>
        <b-button @click="sort('release_date')">Releasedate</b-button>
        <b-button @click="sort('name')">Name</b-button>
        <b-button @click="sort('director')">Director</b-button>
        <b-button @click="sort('producer')">
          Producer <fa v-if="sort" :icon="['fas', 'sort-amount-down']" />
        </b-button>
      </b-button-group>
    </div>
    <b-alert v-if="debug" show variant="warning" class="debug mb-3">
      <strong>Debug:</strong>
      <div>sort={{ currentSort }}</div>
      <div>dir={{ currentSortDir }}</div>
      <div>pageSize={{ pageSize }}</div>
      <div>page={{ currentPage }}</div>
    </b-alert>
    <b-card-group deck>
      <b-card v-for="item in sortedFilms" :key="item.episode_id" class="mb-5">
        <b-list-group>
          <b-list-group-item>
            <b-card-title class="text-primary">
              {{ item.title }}
            </b-card-title>
          </b-list-group-item>
          <b-list-group-item>
            <div class="opening-crawl text-primary">
              {{ item.opening_crawl }}
            </div>
          </b-list-group-item>
          <b-list-group-item>
            <strong>Episode:</strong> {{ item.episode_id }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Director:</strong> {{ item.director }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Producer:</strong> {{ item.producer }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Release Date:</strong> {{ item.release_date }}
          </b-list-group-item>
        </b-list-group>
      </b-card>
    </b-card-group>
    <b-button @click="prevPage">Previous Page</b-button>
    <b-button @click="nextPage">Next Page</b-button>
  </section>
</template>

<script>
// import _ from 'lodash'
import axios from '~/plugins/axios'

export default {
  components: {},
  data() {
    return {
      films: {},
      currentSort: 'episode_id',
      currentSortDir: 'asc',
      pageSize: 4,
      currentPage: 1,
      debug: true,
      sortProducerUp: '',
      sortProducerDown: ''
    }
  },
  computed: {
    // filmsOrderedByID: function() {
    //   const filmsOrdered = _.orderBy(this.films, 'episode_id')
    //   return filmsOrdered
    // },
    sortedFilms: function() {
      // 73:14  error  Unexpected side effect in "sortedFilms" computed property  vue/no-side-effects-in-computed-properties
      // Because: mutates the ORIGINAL array!
      // solution: slice doesnt throw an error, because it builds a copy of it. Noteworthy.
      // return this.films.sort((a, b) => {
      return this.films
        .slice()
        .sort((a, b) => {
          let modifier = 1
          if (this.currentSortDir === 'desc') modifier = -1
          if (a[this.currentSort] < b[this.currentSort]) return -1 * modifier
          if (a[this.currentSort] > b[this.currentSort]) return 1 * modifier
          return 0
        })
        .filter((row, index) => {
          const start = (this.currentPage - 1) * this.pageSize
          const end = this.currentPage * this.pageSize
          if (index >= start && index < end) return true
        })
    }
  },
  // Axios with Async/Await
  async asyncData({ error }) {
    const films = await axios
      .get('films/')
      .then(response => ({
        // Handle Success
        films: response.data.results
      }))
      .catch(e => {
        // Handle Errors, generate 404 Status with Message
        error({
          statusCode: 404,
          message: 'Endpoint could not be resolved'
        })
      })
    return films
  },
  methods: {
    sort: function(sort) {
      // if s == current sort, reverse
      if (sort === this.currentSort) {
        this.currentSortDir = this.currentSortDir === 'asc' ? 'desc' : 'asc'
      }
      this.currentSort = sort
    },
    nextPage: function() {
      if (this.currentPage * this.pageSize < this.films.length)
        this.currentPage++
    },
    prevPage: function() {
      if (this.currentPage > 1) this.currentPage--
    }
  }
}
</script>

<style></style>
