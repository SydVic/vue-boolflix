<template>
  <div class="card" @mouseenter="show = false" @mouseleave="show = true">
    <!-- MOVIE POSTER  -->
    <div v-if="show" class="poster-wrapper">
      <span class="type-label" :class="movie.title? 'text-blue' : 'text-red'">{{movieOrSerie(movie)}}</span>
      <span v-show="posterUnavalaible" class="backup-title">{{ getTitle(movie) }}</span>
      <img class="poster" :src="getPosterImg(movie)" :alt="getOriginalTitle(movie)">
    </div>
    <!-- /MOVIE POSTER  -->

    <!-- MOVIE INFO -->
    <div v-else class="info-wrapper">
      <!-- TITLE -->
      <div class="title">Titolo: 
        <span>{{ getTitle(movie) }}</span>
      </div>
      <!-- ORIGINAL TITLE -->
      <div class="original-title">Titolo originale: 
        <span>{{ getOriginalTitle(movie) }}</span>
      </div>
      <!-- GENRE -->
      <div class="genre">
        {{ createGenresRequest(movie) }}
        <ul>
          <li v-for="item in movieGenres" :key="item.id">Genre: {{ item.name }}</li>
        </ul>
        </div>
      <!-- LANGUAGE -->
      <div class="language">Lingua:
        <img 
        class="flag"
        :src="getFlag(movie)" 
        :alt="movie.original_language">
      </div>
      <!-- RATING -->
      <div class="rating">Voto:
        <span v-for="movie in convertRating(movie.vote_average)" :key="movie.id" class="stars-full">
          <i class="fas fa-star"></i>
        </span>
        <span v-for="movie in (5 - convertRating(movie.vote_average))" :key="movie.id" class="stars-empty">
          <i class="far fa-star"></i>
        </span>
      </div>
      <!-- OVERVIEW -->
      <div class="overview">Overview: 
        <span>{{ movie.overview }}</span>
      </div>
      <!-- CAST -->
      <div class="show-cast" @click="createCastRequest(movie), showCast = !showCast">{{ showCast? "hide main cast" : "show main cast" }}</div>
      <div v-show="showCast" class="cast-wrapper">
        <ul class="cast-list">
          <li v-for="item in movieCast" :key="item.cast_id">{{ item.name }}</li>
        </ul>
      </div>
      <!-- CAST -->
    </div>
    <!-- /MOVIE INFO -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AppCard",
  data: function() {
    return {
      show: true,
      apiKey: "21af1f5df7b829ad53fd11029771d866",
      movieCast: [],
      showCast: false,
      movieGenres: [],
      posterUnavalaible: false,
    }
  },
  props: {
    movie: Object,
  },
  methods: {
    getPosterImg(movie) {
      if (movie.poster_path) {
        return `https://image.tmdb.org/t/p/w342${movie.poster_path}`;
      } else if (movie.backdrop_path) {
        return `https://image.tmdb.org/t/p/w342${movie.backdrop_path}`;
      } else {
        this.posterUnavalaible = true;
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
    movieOrSerie(movie) {
      if (movie.title) {
        return "movie";
      } else {
        return "tv serie";
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
      const convertedNumber = Math.ceil(vote / 2);
      return convertedNumber;
    },
    createCastRequest(movie) {
      const axiosUrl = 'https://api.themoviedb.org/3/movie/'+ movie.id + '/credits?api_key='+ this.apiKey;
      axios.get(axiosUrl).then((resp) => {
        this.movieCast = resp.data.cast.slice(0, 5); 
      });
    },
    createGenresRequest(movie) {
      const axiosUrl = 'https://api.themoviedb.org/3/movie/'+ movie.id +'?api_key='+ this.apiKey;
      axios.get(axiosUrl).then((resp) => {
        this.movieGenres = resp.data.genres;
      });
    },
  },
}
</script>

<style lang="scss" scoped>
@import '~@fortawesome/fontawesome-free/css/all.min.css';

.card {
  color: #ffffff;
  background-color: #000000;
  border: 2px solid #fff5f5;
  text-align: left;
  margin: 10px;
  width: 342px;
  height: 530px;
  overflow: hidden;
  position: relative;

  .poster-wrapper {
    text-align: center;

    .type-label {
      position: absolute;
      top: 10px;
      left: 10px;
      padding: 0.3rem 0.5rem;
      background-color: rgba( #d4d4d4, 0.5);
      font-weight: bold;
      text-transform: uppercase;
      border-radius: 5px;

      &.text-blue {
        color: #0000ff;
      }

      &.text-red {
        color: #ff0000;
      }
    }

    .backup-title {
      position: absolute;
      top: 15%;
      left: 50%;
      transform: translateX(-50%);
      color: black;
      font-size: 1.5rem;
      font-weight: bolder;
    }

    img {
      width: 100%;
      height: 530px;
    }
  }

  .info-wrapper {
    padding: 1.5rem .7rem 1rem .7rem;
    height: 100%;
    overflow-y: auto;

    .title {
      font-weight: bold;

      span {
        color: rgb(231, 231, 231);
      }
    }
    
    .stars-full {
      color: #ffd700;
    }
  
    .flag {
    width: 15px;
    height: 15px;
    }

    .show-cast {
      text-transform: uppercase;
      color: #0000ff;
      cursor: pointer;
      display: inline-block;
    }
  }
}
</style>