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
    <div 
    class="movies-search-result-wrapper"
    v-for="(item) in filmResults" :key="item.id">
      <h2 class="title">{{ item.title }}</h2>
      <h3 class="original-title">{{ item.original_title }}</h3>
      <div class="language">
        <!-- <img 
        v-if="(`./assets/flags/${item.original_language}.png`)"
        class="flag"
        :src="require(`./assets/flags/${item.original_language}.png`)" 
        :alt="item.original_language">
        <h4 v-else>{{item.original_language}}</h4> -->
        <h4>{{item.original_language}}</h4>
      </div>
      <h5 class="rating">{{ item.vote_average }}</h5>
    </div>
    <!-- /WRAPPER DEI RISULTATI DELLA RICERCA FILM -->

    <!-- WRAPPER DEI RISULTATI DELLA RICERCA SERIE TV -->
    <div 
    class="tvseries-search-result-wrapper"
    v-for="(item) in tvSeriesResults" :key="item.id">
      <h2 class="title">{{ item.name }}</h2>
      <h3 class="original-title">{{ item.original_name }}</h3>
      <div class="language">
        <!-- <img 
        v-if="(`./assets/flags/${item.original_language}.png`)"
        class="flag"
        :src="require(`./assets/flags/${item.original_language}.png`)" 
        :alt="item.original_language">
        <h4 v-else>{{item.original_language}}</h4> -->
        <h4>{{item.original_language}}</h4>
      </div>
      <h5 class="rating">{{ item.vote_average }}</h5>
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
      // searchResults: []
    }
  },
  methods: {
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
        // this.searchResults = [...this.filmResults, ...this.tvSeriesResults];
      });      
    },
  }
}
</script>

<style lang="scss">
.flag {
  width:20px;
  height: 20px;
}
</style>
