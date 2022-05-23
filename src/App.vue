<template>
  <div id="app">
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
        console.log(resp);
      });
    }
  }
}
</script>

<style lang="scss">

</style>
