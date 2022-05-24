<template>
  <section class="main">
    <!-- WRAPPER DEI RISULTATI DELLA RICERCA FILM -->
    <div class="movies-search-result-wrapper">
      <div class="film-card" v-for="(item) in filmResults" :key="item.id">
        <img class="poster" :src="`https://image.tmdb.org/t/p/w300${item.poster_path}`" :alt="item.original_title">
        <h2 class="title">{{ item.title }}</h2>
        <h3 class="original-title">{{ item.original_title }}</h3>
        <div class="language">
          <img 
          class="flag"
          :src="getFlag(item)" 
          :alt="item.original_language">
         
          <!-- <h4>{{item.original_language}}</h4> -->
        </div>
        <h5 class="rating">{{ ratingConversion(item.vote_average) }}</h5>
      </div>
    </div>
    <!-- /WRAPPER DEI RISULTATI DELLA RICERCA FILM -->

    <!-- WRAPPER DEI RISULTATI DELLA RICERCA SERIE TV -->
    <div 
    class="tvseries-search-result-wrapper">
      <div class="tv-series-card" v-for="(item) in tvSeriesResults" :key="item.id">
        <img class="poster" :src="`https://image.tmdb.org/t/p/w300${item.poster_path}`" :alt="item.original_name">
        <h2 class="title">{{ item.name }}</h2>
        <h3 class="original-title">{{ item.original_name }}</h3>
        <div class="language">
          <img 
          class="flag"
          :src="getFlag(item)" 
          :alt="item.original_language">
        </div>
        <h5 class="rating">{{ ratingConversion(item.vote_average) }}</h5>
      </div>
    </div>
    <!-- /WRAPPER DEI RISULTATI DELLA RICERCA SERIE TV -->
  </section>
</template>

<script>
export default {
  name: "AppMain",
  methods: {
    getFlag(item) {
      const lang = item.original_language;
      if (['it', 'en', 'de', 'es', 'fr'].includes(lang)) {
        return require(`../assets/flags/${item.original_language}.png`)
      } else {
        return item.original_language;
      }
    },
    convertRating(vote) {
      const convertedNumber = Math.round(vote / 2);
      return convertedNumber;
    },
  },
}
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

.main {
  height: calc(100vh - $header-height);
  background-color: black;

  .movies-search-result-wrapper {
  display: flex;
  flex-wrap: wrap;
  }

  .tvseries-search-result-wrapper {
  display: flex;
  flex-wrap: wrap;
  }

  .flag {
  width:20px;
  height: 20px;
  }
}
</style>