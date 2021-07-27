<template>
  <div class="movies-edit">
    <h1>{{ message }}</h1>
    <form class="flex-down" v-on:submit.prevent="updateMovie()">
      <label for="title">Title</label>
      <input id="title" type="text" v-model="currentMovieParams.title" />
      <hr style="width: 25%" />
      <label for="year">Year</label>
      <input id="year" type="number" style="font-family: arial" v-model="currentMovieParams.year" />
      <hr style="width: 25%" />
      <label for="plot">Plot</label>
      <input id="plot" type="text" v-model="currentMovieParams.plot" />
      <hr style="width: 25%" />
      <label for="director">Director</label>
      <input id="director" type="text" v-model="currentMovieParams.director" />
      <hr style="width: 25%" />
      <label for="english">English</label>
      <input id="english" type="checkbox" v-model="currentMovieParams.english" />

      <input type="submit" value="submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome Affagatto",
      currentMovieParams: { english: false },
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response);
      this.currentMovieParams = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios.patch(`/movies/${this.$route.params.id}`, this.currentMovieParams).then((response) => {
        this.$router.push(`/movies/${response.data.id}`);
        console.log(response.data);
      });
    },
  },
};
</script>

<style>
.flex-down {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-between;
}
.flex-down * {
  margin: 10px;
}
</style>
