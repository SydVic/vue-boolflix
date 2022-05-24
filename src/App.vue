<template>
  <div id="app">
    <AppHeader @modifiedInput="startSearch"/>
    <AppMain :movies="moviesResults" :tvSeries="tvSeriesResults"/>
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
      moviesResults: [],
      tvSeriesResults: [],
    }
  },
  methods: {
    startSearch(keyword) {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: this.apiKey,
          query: keyword
        }
      })
      .then((resp) => {
        this.moviesResults = resp.data.results;
      });
      axios.get('https://api.themoviedb.org/3/search/tv', {
        params: {
          api_key: this.apiKey,
          query: keyword
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


</style>
