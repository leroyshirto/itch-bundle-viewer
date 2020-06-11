<template>
  <section class="section">
    <b-loading :is-full-page="true" :active.sync="isLoading"></b-loading>
    <section class="section">
      <b-field label="Enter Bundle id" label-position="inside" grouped>
        <b-input v-model="bundleId"></b-input>
        <p class="control">
          <b-button class="button is-primary" @click="downloadBundleJson(bundleId)" :disabled="bundleId===''">Search</b-button>
        </p>
      </b-field>
      <p>Bundle is sorted by number of ratings</p>
    </section>
    <section class="section">
      <div class="columns is-multiline">
        <div class="column is-one-quarter" v-for="gameData in sortedGames" :key="gameData.id">
          <game-card :game-data="gameData"></game-card>
        </div>
      </div>
    </section>
  </section>
</template>

<script>
import { orderBy } from 'lodash'
import GameCard from '@/components/GameCard'

export default {
  name: 'Home',
  components: { GameCard },
  data () {
    return {
      isLoading: false,
      bundleId: '',
      bundleData: []
    }
  },
  computed: {
    sortedGames () {
      return orderBy(this.bundleData, 'ratings_count', 'desc')
    }
  },
  methods: {
    downloadBundleJson (bundleId) {
      if (bundleId) {
        this.isLoading = true
        fetch(`https://cors-anywhere.herokuapp.com/https://itch.io/bundle/${bundleId}/games.json`,
          {
            headers: {
              Accept: 'application/json'
            }
          })
          .then(response => response.json())
          .then(json => {
            this.bundleData = json.games
            this.isLoading = false
          })
      }
    }
  }
}
</script>
