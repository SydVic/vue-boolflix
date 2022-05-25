<template>
  <div id="app">
    <AppHeader 
    @modifiedInput="startSearch"
    :moviesGenres="movieGenresReference"
    :tvGenres="tvGenresReference"/>
    <AppMain 
    :movies="moviesResults" 
    :tvSeries="tvSeriesResults"/>
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
      movieGenresReference: [],
      tvGenresReference: [],
    }
  },
  methods: {
    startSearch(keyword) {
      const options = {
        params: {
          api_key: this.apiKey,
          query: keyword,
        },
      };
      const request1 = axios.get("https://api.themoviedb.org/3/search/movie", options);
      const request2 = axios.get("https://api.themoviedb.org/3/search/tv", options);
      const request3 = axios.get("https://api.themoviedb.org/3/genre/movie/list?api_key=21af1f5df7b829ad53fd11029771d866");
      const request4 = axios.get("https://api.themoviedb.org/3/genre/tv/list?api_key=21af1f5df7b829ad53fd11029771d866");

      axios.all([request1, request2, request3, request4]).then(resp => {
        this.moviesResults = resp[0].data.results;
        this.tvSeriesResults = resp[1].data.results;
        this.movieGenresReference = resp[2].data.genres;
        this.tvGenresReference = resp[3].data.genres;
      });
      // axios.get('https://api.themoviedb.org/3/search/movie', {
      //   params: {
      //     api_key: this.apiKey,
      //     query: keyword
      //   }
      // })
      // .then((resp) => {
      //   this.moviesResults = resp.data.results;
      // });
      // axios.get('https://api.themoviedb.org/3/search/tv', {
      //   params: {
      //     api_key: this.apiKey,
      //     query: keyword
      //   }
      // })
      // .then((resp) => {
      //   this.tvSeriesResults = resp.data.results;
      // });      
    },
  },
}
</script>

<style lang="scss">
@import "./style/common.scss";

</style>
