<template>
  <section class="main">
    <div class="container">
      <AppCard v-for="item in movies" :key="item.id" :movie="item"/>
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

  .container {
    margin: 0 auto;
    padding: 2rem 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    width: 95%;
  }
}
</style>