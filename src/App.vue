<template>
  <div id="app">
    <!-- WRAPPER DELLA RICERCA -->
    <div class="search-wrapper">
      <input 
      class="search-input" 
      type="text" 
      placeholder="titolo film o parola chiave"
      v-model="searchInput">

      <button 
      class="search-btn"
      @click="startSearch"
      >Premi per avviare la ricerca</button>
    </div>
    <!-- /WRAPPER DELLA RICERCA -->

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
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  components: {

  },
  data: function() {
    return {
      apiKey: "21af1f5df7b829ad53fd11029771d866",
      searchInput: "",
      filmResults: [],
      tvSeriesResults: [],
    }
  },
  methods: {
    getFlag(item) {
      const lang = item.original_language;
      if (['it', 'en', 'de', 'es', 'fr'].includes(lang)) {
        return require(`./assets/flags/${item.original_language}.png`)
      } else {
        return item.original_language;
      }
    },
    startSearch() {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: this.apiKey,
          query: this.searchInput
        }
      })
      .then((resp) => {
        this.filmResults = resp.data.results;
      });
      axios.get('https://api.themoviedb.org/3/search/tv', {
        params: {
          api_key: this.apiKey,
          query: this.searchInput
        }
      })
      .then((resp) => {
        this.tvSeriesResults = resp.data.results;
      });      
    },
    ratingConversion(vote) {
      const convertedNumber = Math.round(vote / 2);
      return convertedNumber;
    }
  }
}
</script>

<style lang="scss">
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
</style>
