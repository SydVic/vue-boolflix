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

    <!-- WRAPPER DEI RISULTATI DELLA RICERCA -->
    <div 
    class="serach-result-wrapper"
    v-for="(item, index) in searchResults" :key="index">
      <span>{{ index + 1 }}</span>
      <h2 class="title">{{ item.title }}</h2>
      <h3 class="original-title">{{ item.original_title }}</h3>
      <h4 class="language">{{ item.original_language }}</h4>
      <h5 class="rating">{{ item.vote_average }}</h5>
    </div>
    <!-- /WRAPPER DEI RISULTATI DELLA RICERCA -->
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
      searchResults: []
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
        this.searchResults = resp.data.results;
      });
    }
  }
}
</script>

<style lang="scss">

</style>
