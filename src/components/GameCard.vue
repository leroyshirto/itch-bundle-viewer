<template>
  <div class="card">
    <div class="card-image">
        <a :href="gameData.url" target="_blank">
          <figure class="image is-4by3">
          <img :src="gameData.cover" alt="Game Cover" loading="lazy">
          </figure>
        </a>
    </div>
    <div class="card-content">
        <div class="media">
        <div class="media-content">
            <p class="title is-4">{{gameData.title}}</p>
            <p class="subtitle is-6"><a :href="gameData.user.url" target="_blank">{{gameData.user.name}}</a> Ratings: {{gameData.ratings_count}} <br> Price: {{formatedPrice(gameData.price)}}</p>
        </div>
        </div>

        <div class="content">
          {{gameData.short_text}}
          <b-taglist>
            <b-tag type="is-info" v-for="(platform, index) in gameData.platforms" :key="index">{{platform}}</b-tag>
          </b-taglist>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameCard',
  props: {
    gameData: Object
  },
  methods: {
    formatedPrice (price) {
      if (!price) {
        return 'FREE'
      }

      return price
    }
  }
}
</script>

<style scoped>

</style>
