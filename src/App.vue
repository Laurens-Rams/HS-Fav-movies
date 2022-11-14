<script setup>
import { ref } from 'vue';
import movies from './assets/movies.json';

const favoriteMovie = ref('');
const watchedList = ref([]);

function calculateStars(movie){
  return Math.floor(movie.score / 20)
}

</script>
<template>
    <h3>Movie list</h3>
      <ul class="all_cards">
        <li v-for="movie in movies" :key="movies.id">
            <div class="movie_card">
              <div class="picture"><img :src="movie.picture" alt="test"/></div>
              <p class="title">{{ movie.title }}</p>
              <div class="score"><p class="stars" v-for="i in calculateStars(movie)">☆</p></div>
              <p class="fav-icon" v-show="favoriteMovie === movie.title">😍</p>
              <input class="watched_input" type="checkbox" :id="movie.id" :value="movie.title" v-model="watchedList" /> 
            </div>
        </li>
      </ul>
    <hr />

    <h3>Controls</h3>

    <div class="all_controlls">
    <div class="fav_mov">
      <span><h4><strong>MY FAV MOVIE: </strong>{{ favoriteMovie || 'none chosen yet :(' }}</h4></span>
      <br />
      <br />
      <select v-model="favoriteMovie">
        <option disabled value="">Please select a favorite!</option>
        <option v-for="favmovie in movies" :key="movies.id">
        {{ favmovie.title }}
      </option>
      </select>
    </div>

    <div class="watched_mov">
      <span><h4>Movies watched this year: {{ watchedList.toString() }}</h4></span>
      <br />
      <br />
      <select id="select_two" v-model="watchedList" multiple>
        <option v-for="watchedMovie in movies" :key="movies.id">
        {{ watchedMovie.title }}
      </option>
      </select>
    </div>

    <div class="watched_mov">
      <span><h4>Movies watched this year: {{ watchedList.toString() }}</h4></span>
      <br />
      <br />
      <div v-for="movie in movies" :key="movie.id">
        <input class="watched_input small" type="checkbox" :id="movie.id" :value="movie.title" v-model="watchedList">
        <label>{{ movie.title}}</label>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
