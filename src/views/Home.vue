<template>
  <div class="home">
    <h2>Movies</h2>
    <div>
      <p>Name: <input type="text" v-model="newMovie.name"></p>
      <p>Duration: <input type="text" v-model="newMovie.duration"></p>
      <p>Photo URL: <input type="text" v-model="newMovie.photo"></p>
      <button v-on:click="createMovie()">Create Movie</button>
      <hr>
    </div>
    <div v-for="movie in movies">
      <img v-bind:src="movie.photo">
      <p>Name: {{ movie.name }}</p>
      <p>Duration: {{ movie.duration }}</p>
      <hr>
    </div>

  </div>
</template>

<style>
  img {
    width: 250px;
  }
</style>

<script>
// @ is an alias to /src
import axios from "axios";

export default {
  data: function() {
    return {
      movies: [],
      newMovie: {
        name: "",
        duration: "",
        photo: ""
      }
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
    });
  },
  methods: {
    createMovie: function() {
      var params = {
        name: this.newMovie.name,
        duration: this.newMovie.duration,
        photo: this.newMovie.photo
      }
      axios.post("/api/movies", params).then(response => {
        console.log(response);
        this.movies.push(response.data);
      });
    }
  }
};
</script>

