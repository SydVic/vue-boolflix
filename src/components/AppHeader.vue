<template>
  <section class="header">
    <div class="logo">
      boolflix
    </div>
    <!-- WRAPPER DELLA RICERCA -->
    <div class="search-wrapper">
      <input 
      class="search-input" 
      type="text" 
      placeholder="title or keyword"
      v-model="searchInput">

      <button 
      class="search-btn"
      @click="veirfyAndSendSearch()"
      >Search
      </button>

      <select 
      class="movies-filter" 
      name="movies-filter" 
      id="" 
      @change="$emit('movieGenreChanged', selectedMovieGenre)" v-model="selectedMovieGenre">
        <option value="">Filter Movies for genre</option>
        <option :value="item.id" v-for="item in moviesGenres" :key="item.id">{{item.name}}</option>
      </select>
      <select 
      class="tv-series-filter" 
      name="tv-series-filter" 
      id="" 
      @change="$emit('tvGenreChanged', selectedTvGenre)" 
      v-model="selectedTvGenre">
        <option value="">Filter TvSeries for genre</option>
        <option :value="item.id" v-for="item in tvGenres" :key="item.id">{{item.name}}</option>
      </select>
    </div>
    <!-- /WRAPPER DELLA RICERCA -->
  </section>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    moviesGenres: Array,
    tvGenres: Array,
  },
  data() {
    return {
      searchInput: "",
      selectedMovieGenre: "",
      selectedTvGenre: "",
    }
  },
  methods: {
    veirfyAndSendSearch() {
      if (this.searchInput.trim()) {
        this.$emit('modifiedInput', this.searchInput);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

.header {
  height: $header-height;
  background-color: rgb(36, 35, 35);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;

  .logo {
    color: red;
    text-transform: uppercase;
    font-size: 2rem;
    font-weight: bolder;
  }

  .search-input {
    padding: .5rem .7rem;
    border: 2px solid red;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
  }

  .search-btn {
    padding: .5rem .7rem;
    border: 2px solid red;
    background-color: red;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
    margin-right: 1.5rem;
    text-transform: uppercase;
    font-weight: bold;
  }

  .movies-filter {
    padding: .4rem .2rem;
    border-radius: 8px;
    margin-right: .5rem;
    border: 2px solid red;
  }

  .tv-series-filter {
    padding: .4rem .2rem;
    border-radius: 8px;
    border: 2px solid red;
  }
}
</style>