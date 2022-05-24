<template>
  <section class="main">
    <div class="movies-container">
      <AppCard v-for="item in movies" :key="item.id" :movie="item"/>
    </div>
    <!-- <div class="tvseries-container">
      <AppCard v-for="item in tvSeries" :key="item.id" :tvSerie="item"/>
    </div> -->
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
  background-color: black;
  overflow-y: auto;

  .movies-container {
    display: flex;
    flex-wrap: wrap;
  }

  .tvseries-container {
    display: flex;
    flex-wrap: wrap;
  }
}
</style>