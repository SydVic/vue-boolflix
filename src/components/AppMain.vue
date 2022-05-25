<template>
  <section class="main">
    <h2 class="movies">MOVIES</h2>
    <div class="movies-container">
      <AppCard v-for="item in movies" :key="item.id" :movie="item"/>
    </div>
    <h2 class="tv-series">TV SERIES</h2>
    <div class="tv-series-container">
      <AppCard v-for="item in tvSeries" :key="item.id" :movie="item"/>
    </div>
  </section>
</template>

<script>
import AppCard from "./AppCard.vue";

export default {
  name: "AppMain",
  components: {
    AppCard,
  },
  props: {
    movies: Array,
    tvSeries: Array,
  }, 
}
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

.main {
  width: 100%;
  height: calc(100vh - $header-height);
  background-color: rgb(97, 97, 97);
  overflow-y: auto;
  text-align: center;

  h2 {
    color: #ffffff;
  }

  .movies-container {
    margin: 0 auto;
    padding: 2rem 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    width: 97%;
    border: 2px solid blue;
  }

  .tv-series-container {
    margin: 0 auto;
    padding: 2rem 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    width: 97%;
    border: 2px solid rgb(185, 14, 14);
  }
}
</style>