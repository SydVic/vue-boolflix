<template>
  <div class="card">
    <!-- <img class="poster" :src="`https://image.tmdb.org/t/p/w300${movie.poster_path}`" :alt="getOriginalTitle(movie)"> -->
    <!-- <img class="poster" :src="`https://image.tmdb.org/t/p/w342${movie.backdrop_path}`" :alt="getOriginalTitle(movie)"> -->
    <img class="poster" :src="getPosterImg(movie)" :alt="getOriginalTitle(movie)">
    <h2 class="title">{{ getTitle(movie) }}</h2>
    <h3 class="original-title">{{ getOriginalTitle(movie) }}</h3>
    <div class="language">
      <img 
      class="flag"
      :src="getFlag(movie)" 
      :alt="movie.original_language">
    </div>
      <!-- <h5 class="rating">{{ convertRating(movie.vote_average) }} -->
        <!-- <span v-for="n in convertRating(movie.vote_average)" :key="n" class="stars-full">
          <i class="fas fa-star"></i>
        </span>
        <span v-for="n in (5 - convertRating(movie.vote_average))" :key="n" class="stars-empty">
          <i class="far fa-star"></i>
        </span> -->
      <!-- </h5> -->
  </div>
</template>

<script>
export default {
  name: "AppCard",
  props: {
    movie: Object,
  },
  methods: {
    getPosterImg(movie) {
      if (movie.poster_path) {
        return `https://image.tmdb.org/t/p/w342${movie.poster_path}`;
      } else if (movie.backdrop_path)
      {
        return `https://image.tmdb.org/t/p/w342${movie.backdrop_path}`;
      } else {
        return require('../assets/img/poster-holder.jpg');
      }
    },
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
@import '~@fortawesome/fontawesome-free/css/all.min.css';

.card {
  color: white;
  background-color: #808080;
  text-align: center;
  margin: 10px;
  padding: 10px;
  width: calc(100% / 4 - 20px);

  img {
    width: 100%;
  }

  .stars-full {
    color: #ffd700;
  }

  .flag {
  width:20px;
  height: 20px;
  }
}
</style>