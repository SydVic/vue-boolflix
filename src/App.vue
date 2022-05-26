<template>
  <div id="app">
    <AppHeader 
    @modifiedInput="startSearch($event)"
    @movieGenreChanged="saveSelectedMovieGenre"
    @tvGenreChanged="saveSelectedTvGenre"
    :moviesGenres="movieGenresReference"
    :tvGenres="tvGenresReference"/>
    <AppMain 
    :movies="filteredMovies"
    :tvSeries="filteredTvSeries"/>
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
      savedSelectedMovieGenre: "",
      savedSelectedTvGenre: "",
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

      axios.all([request1, request2]).then(resp => {
        this.moviesResults = resp[0].data.results;
        this.tvSeriesResults = resp[1].data.results;
      });     
    },
    saveSelectedMovieGenre(selectedGenre) {
      this.savedSelectedMovieGenre = selectedGenre;
    },
    saveSelectedTvGenre(selectedGenre) {
      this.savedSelectedTvGenre = selectedGenre;
    }
  },
  computed: {
    filteredMovies() {
      if (this.savedSelectedMovieGenre === "") {
        return this.moviesResults;
      } else {
        return this.moviesResults.filter(item => {
        return item.genre_ids.includes(this.savedSelectedMovieGenre);
        })
      }
    },
    filteredTvSeries() {
      if (this.savedSelectedTvGenre === "") {
        return this.tvSeriesResults;
      } else {
        return this.tvSeriesResults.filter(item => {
        return item.genre_ids.includes(this.savedSelectedTvGenre);
        })
      }
    }
  },
  created() {
    const request1 = axios.get("https://api.themoviedb.org/3/genre/movie/list?api_key=21af1f5df7b829ad53fd11029771d866");
    const request2 = axios.get("https://api.themoviedb.org/3/genre/tv/list?api_key=21af1f5df7b829ad53fd11029771d866");

    axios.all([request1, request2]).then(resp => {
    this.movieGenresReference = resp[0].data.genres;
    this.tvGenresReference = resp[1].data.genres;
    });
  }
}
</script>

<style lang="scss">
@import "./style/common.scss";

</style>
