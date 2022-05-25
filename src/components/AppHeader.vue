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
      placeholder="titolo o parola chiave"
      v-model="searchInput">

      <button 
      class="search-btn"
      @click="$emit('modifiedInput', searchInput)"
      >Premi per avviare la ricerca
      </button>

      <select class="movies-filter" name="movies-filter" id="">
        <option value="">Filtra film per genere</option>
        <option value="moviesGenres.id" v-for="item in moviesGenres" :key="item.id">{{item.name}}</option>
      </select>
      <select class="tv-series-filter" name="tv-series-filter" id="">
        <option value="">Filtra serie tv per genere</option>
        <option value="tvGenres.id" v-for="item in tvGenres" :key="item.id">{{item.name}}</option>
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
    padding: .3rem .3rem;
    margin-right: .3rem;
    border-radius: 5px;
  }

  .search-btn {
    padding: .3rem .3rem;
    border-radius: 5px;
  }

  .movies-filter {
    padding: .2rem .2rem;
    border-radius: 5px;
  }

  .tv-series-filter {
    padding: .2rem .2rem;
    border-radius: 5px;
  }
}
</style>