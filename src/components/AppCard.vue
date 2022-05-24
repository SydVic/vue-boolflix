<template>
  <div class="card" @mouseenter="show = false" @mouseleave="show = true">
    <div v-if="show" class="img-wraper">
      <img class="poster" :src="getPosterImg(movie)" :alt="getOriginalTitle(movie)">
    </div>
    <div v-else class="info-wrapper">
      <div class="title">Titolo: 
        <span>{{ getTitle(movie) }}</span>
      </div>
      <div class="original-title">Titolo originale: 
        <span>{{ getOriginalTitle(movie) }}</span>
      </div>
      <div class="language">Lingua:
        <img 
        class="flag"
        :src="getFlag(movie)" 
        :alt="movie.original_language">
      </div>
      <div class="rating">Voto:
        <span v-for="movie in convertRating(movie.vote_average)" :key="movie.id" class="stars-full">
          <i class="fas fa-star"></i>
        </span>
        <span v-for="movie in (5 - convertRating(movie.vote_average))" :key="movie.id" class="stars-empty">
          <i class="far fa-star"></i>
        </span>
      </div>
      <div class="overview">Overview: 
        <span>{{ movie.overview }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppCard",
  data: function() {
    return {
      show: true,
    }
  },
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
  background-color: #000000;
  border: 2px solid rgb(255, 245, 245);
  text-align: left;
  margin: 10px;
  width: 342px;
  min-height: 510px;

  img {
    width: 100%;
    height: auto;
  }

  .info-wrapper {
    padding: 1.5rem .7rem 0 .7rem;
    
    .stars-full {
      color: #ffd700;
    }
  
    .flag {
    width:20px;
    height: 20px;
    }
  }
}
</style>