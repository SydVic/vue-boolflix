<template>
  <div id="app">
    <AppHeader @modifiedInput="saveSearchInput($event)"/>
    <AppMain />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue"
import axios from "axios";

export default {
  name: 'App',
  components: {
    AppHeader,
    AppMain,
  },
  data: function() {
    return {
      apiKey: "21af1f5df7b829ad53fd11029771d866",
      savedSearchInput: "",
      filmResults: [],
      tvSeriesResults: [],
    }
  },
  methods: {
    saveSearchInput(searchInput) {
      this.savedSearchInput = searchInput;
    },
    startSearch() {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: this.apiKey,
          query: this.savedSearchInput
        }
      })
      .then((resp) => {
        this.filmResults = resp.data.results;
      });
      axios.get('https://api.themoviedb.org/3/search/tv', {
        params: {
          api_key: this.apiKey,
          query: this.savedSearchInput
        }
      })
      .then((resp) => {
        this.tvSeriesResults = resp.data.results;
      });      
    },
  },
}
</script>

<style lang="scss">
@import "./style/common.scss";

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
