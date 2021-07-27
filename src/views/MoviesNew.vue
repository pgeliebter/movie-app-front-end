<template>
  <div class="movies-new">
    <h1>This is a new page</h1>
    <form v-on:submit.prevent="newMovie()">
      <div>
        Title:
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        Plot:
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      <div>
        Year:
        <input type="number" min="1901" max="2025" v-model="newMovieParams.year" />
      </div>
      <div>
        Director:
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <div>
        English:
        <input value="null" type="checkbox" v-model="newMovieParams.english" />
      </div>
      <div>
        <input type="submit" />
      </div>
      <hr style="width: 25%" />
      <div>
        <input type="reset" />
      </div>
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: { english: false },
    };
  },
  methods: {
    newMovie: function () {
      console.log(this.newMovieParams);
      axios.post("http://localhost:3000/movies", this.newMovieParams).then((response) => {
        console.log(response.data, response.errors);
      });
    },
  },
};
</script>
