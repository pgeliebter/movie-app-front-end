<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <div>
      <button v-on:click="indexMovies()">Load Movies</button>
      <ol>
        <h2>Movies</h2>
        <li v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</li>
      </ol>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Hello wosdafrasdfasdfld!",
      movies: [],
    };
  },
  // created: function () {
  //   this.indexMovies();
  // },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log(response.data);
      });
    },
  },
};
</script>
