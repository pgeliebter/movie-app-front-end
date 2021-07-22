<template>
  <div class="movies-index">
    <h1>This is an index page</h1>
    <div v-for="movie in movies" :key="movie.id">
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
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
  },
};
</script>
