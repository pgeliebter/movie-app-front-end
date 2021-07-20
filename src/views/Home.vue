<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <div>
      <button v-on:click="newMovie()">New Movies</button>
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
      params: {},
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
    newMovie: function () {
      this.params.title = "hello";
      this.params.year = 1999;
      this.params.plot = "a movie about greetings";
      this.params.english = true;
      console.log(this.params);
      axios
        .post("http://localhost:3000/movies", this.params)
        .then((response) => {
          this.movies = response.data;
          console.log("Success!", response.data);
          this.indexMovies();
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
