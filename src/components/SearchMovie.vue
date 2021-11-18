<template>
  <div class="searchbox">
    <input v-model="searchString" type="search" placeholder="Search a movie" />

    <button @click="$emit('search-movie', searchString)">Search</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      movies: [],
      searchString: "",
    };
  },

  mounted() {
    this.callAPI();
  },

  methods: {
    callAPI() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=b8a9c9466f2868b183c2e2880382011d&language=en-US&query=ritorno"
        )
        .then((r) => {
          this.movies = r.data.results;
        })
        .catch((error) => {
          console.log(error, "ERROR");
        });
    },
  },
};
</script>

<style>
</style>