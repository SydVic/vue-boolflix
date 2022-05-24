<template>
  <div class="card">
    <img class="poster" :src="`https://image.tmdb.org/t/p/w300${movie.poster_path}`" :alt="getOriginalTitle(movie)">
    <!-- <h2 class="title">{{ movie.title }}</h2> -->
    <h2 class="title">{{ getTitle(movie) }}</h2>
    <h3 class="original-title">{{ getOriginalTitle(movie) }}</h3>
    <div class="language">
      <img 
      class="flag"
      :src="getFlag(movie)" 
      :alt="movie.original_language">
      </div>
      <h5 class="rating">{{ convertRating(movie.vote_average) }}</h5>
  </div>
</template>

<script>
export default {
  name: "AppCard",
  props: {
    movie: Object,
  },
  methods: {
    getFlag(movie) {
      const lang = movie.original_language;
      if (['it', 'en', 'de', 'es', 'fr'].includes(lang)) {
        return require(`../assets/flags/${movie.original_language}.png`)
      } else {
        return movie.original_language;
      }
    },
    getTitle(movie) {
      if (movie.title) {
        return movie.title;
      } else {
        return movie.name;
      }
    },
    getOriginalTitle(movie) {
      if (movie.original_title) {
        return movie.original_title;
      } else {
        return movie.original_name;
      }
    },
    convertRating(vote) {
      const convertedNumber = Math.round(vote / 2);
      return convertedNumber;
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  color: white;
  background-color: #808080;
  text-align: center;
  margin: 10px;
  padding: 10px;
  width: calc(100% / 5 - 20px);

  img {
    width: 100%;
  }

  .flag {
  width:20px;
  height: 20px;
  }
}
</style>