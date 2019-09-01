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
        <b-button @click="sortByTitle = !sortByTitle">Title</b-button>
        <b-button @click="sortByEpisode = !sortByEpisode">Episode</b-button>
        <b-button @click="sortByDate = !sortByDate">Releasedate</b-button>
        <b-button @click="sortByDirector = !sortByDirector">Director</b-button>
        <b-button @click="sortByProducer = !sortByProducer">Producer</b-button>
      </b-button-group>
    </div>
    <b-alert v-if="debug" show variant="warning" class="debug mb-3">
      <strong>Debug:</strong>
    </b-alert>
    <b-card-group deck>
      <b-card v-for="item in listView" :key="item.episode_id" class="mb-5">
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
            <strong>Release Date:</strong> {{ item.release_date }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Director:</strong> {{ item.director }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Producer:</strong> {{ item.producer }}
          </b-list-group-item>
        </b-list-group>
      </b-card>
    </b-card-group>
  </section>
</template>

<script>
import _ from 'lodash'
import axios from '~/plugins/axios'

export default {
  components: {},
  data() {
    return {
      films: {},
      // item: {},
      // currentSort: 'episode_id',
      // currentSortDir: 'asc',
      // pageSize: 4,
      // currentPage: 1,
      debug: true,
      // Testing
      filterByName: {},
      filterByStatus: {},
      sortByTitle: false,
      sortByEpisode: false,
      sortByDate: false,
      sortByDirector: false,
      sortByProducer: false
    }
  },
  computed: {
    // listView: function() {
    //   const self = this
    //   if (self.filterByName.length > 0 || self.filterByStatus.length > 0) {
    //     return self.films.filter(function(item) {
    //       return self.sortByEpisode
    //       // self.filterByName.indexOf(item.name) > -1 ||
    //       //   self.filterByStatus.indexOf(item.status) > -1
    //     })
    //   } else {
    //     return self.sortByEpisode
    //   }
    // },
    listView: function() {
      const listView = _.orderBy(this.films, 'episode_id')
      return listView
    }
  },
  watch: {
    sortByTitle: function(val) {
      const self = this
      self.listView = self.sortBy(self.listView, 'title', val)
    },
    sortByEpisode: function(val) {
      const self = this
      self.listView = self.sortBy(self.listView, 'episode_id', val)
    },
    sortByDate: function(val) {
      const self = this
      self.listView = self.sortBy(self.listView, 'release_date', val)
    },
    sortByDirector: function(val) {
      const self = this
      self.listView = self.sortBy(self.listView, 'director', val)
    },
    sortByProducer: function(val) {
      const self = this
      self.listView = self.sortBy(self.listView, 'producer', val)
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
    sortBy: function(array, param, reverse) {
      let filterA, filterB
      return array.sort(function(a, b) {
        switch (param) {
          case 'episode_id':
            filterA = a.episode_id
            filterB = b.episode_id
            break
          case 'title':
            filterA = a.title
            filterB = b.title
            break
          case 'release_date':
            filterA = a.release_date
            filterB = b.release_date
            break
          case 'director':
            filterA = a.director
            filterB = b.director
            break
          case 'producer':
            filterA = a.producer
            filterB = b.producer
            break
        }
        if (reverse) {
          return filterA > filterB ? 1 : -1
        } else {
          return filterA < filterB ? 1 : -1
        }
      })
    }
  }
}
</script>

<style></style>
