<template>
  <div class="movies-show">
    <input type="text" placeholder="Enter a Movie ID" v-model="movieId" />
    <button v-on:click="showMovies()">Show Movie</button>
    <h2>Title: {{ movie.title }}</h2>
    <p>Plot: {{ movie.plot }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <div>
      <p>Actors:</p>
      <ul>
        <li v-for="actor in movie.actors_hash" :key="actor.id">{{ actor.firstName }} {{ actor.lastName }}</li>
      </ul>
    </div>
    <router-link :to="`/movies/${movie.id}/edit`"><button>Fuggehdaboutit</button></router-link>
    <router-link to="/movies">Back to all movies</router-link>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: [],
      movieId: null,
    };
  },
  created: function () {
    axios.get(`http://localhost:3000/movies/${this.$route.params.id}`).then((response) => {
      this.movie = response.data;
      console.log("Movie:", this.movie);
    });
  },
};
</script>
