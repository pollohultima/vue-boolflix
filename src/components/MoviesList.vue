<template>
  <div class="moviesList">
    <SearchMovie
      class="m-3"
      :searchString="searchText"
      @search-movie="search"
    />
    <div class="container">
      <div class="row">
        <div class="col-2" v-for="movie in movies" :key="movie.id">
          <h4 class="text-center">{{ movie.title }}</h4>
          <h5 class="text-center">{{ movie.original_title }}</h5>
          <h6>Language: {{ movie.original_language }}</h6>
          <h6>Rating: {{ movie.vote_average }}</h6>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchMovie from "./SearchMovie.vue";

export default {
  components: {
    SearchMovie,
  },

  data() {
    return {
      movies: [],
      searchText: "",
    };
  },

  methods: {
    search(text) {
      this.searchText = text;
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=b8a9c9466f2868b183c2e2880382011d&query=${this.searchText}`
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