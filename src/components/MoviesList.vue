<template>
  <div class="moviesList">
    <Search :searchString="searchText" @search="search" />
    <div class="container-fluid">
      <h2 class="text-white">Movies:</h2>
      <div class="row g-3">
        <div class="col-2" v-for="movie in movies" :key="movie.id">
          <div class="card d-flex flex-column p-2">
            <img
              v-if="movie.poster_path !== null"
              :src="`https://image.tmdb.org/t/p/w342/${movie.poster_path}`"
              alt=""
            />
            <img
              class="img-fluid"
              v-else
              src="https://www.salonlfc.com/wp-content/uploads/2018/01/image-not-found-1-scaled.png"
              :alt="movie.title"
            />

            <h4 class="text-center text-white">{{ movie.title }}</h4>
            <h5 class="text-center text-white">{{ movie.original_title }}</h5>
            <div class="laguage_wrapper">
              <div class="text-white">Language:</div>
              <div v-if="movie.original_language === 'en'">
                <flag iso="gb" />
              </div>
              <div v-if="movie.original_language === 'ko'">
                <flag iso="kr" />
              </div>
              <div v-if="movie.original_language === 'ja'">
                <flag iso="jp" />
              </div>
              <div v-if="movie.original_language === 'zh'">
                <flag iso="cn" />
              </div>
              <div v-else>
                <flag :iso="movie.original_language" />
              </div>
            </div>

            <div class="d-flex">
              <h6>Rating:</h6>
              <div
                v-for="star in Math.round(movie.vote_average / 2)"
                :key="star"
              >
                <font-awesome-icon icon="star" class="gold" />
              </div>
              <div
                v-for="star in 5 - Math.round(movie.vote_average / 2)"
                :key="star"
              >
                <font-awesome-icon icon="star" class="gray" />
              </div>
            </div>
          </div>
        </div>
      </div>
      <h2 class="text-white">TV Series:</h2>
      <div class="row g-2">
        <div class="col-2" v-for="show in shows" :key="show.id">
          <div class="card d-flex flex-column p-2">
            <img
              v-if="show.poster_path !== null"
              :src="`https://image.tmdb.org/t/p/w342/${movie.poster_path}`"
              alt=""
            />
            <img
              class="img-fluid"
              v-else
              src="https://www.salonlfc.com/wp-content/uploads/2018/01/image-not-found-1-scaled.png"
              :alt="movie.title"
            />
            <h4 class="text-center">{{ show.name }}</h4>
            <h5 class="text-center">{{ show.original_name }}</h5>
            <div>
              <span><h6>Language:</h6></span>
              <div v-if="show.original_language === 'en'">
                <flag iso="gb" />
              </div>
              <div v-if="show.original_language === 'ko'">
                <flag iso="kr" />
              </div>
              <div v-if="show.original_language === 'ja'">
                <flag iso="jp" />
              </div>
              <div v-else-if="show.original_language === 'zh'">
                <flag iso="cn" />
              </div>
              <div v-else>
                <flag :iso="show.original_language" />
              </div>
            </div>
            <div class="d-flex">
              <h6>Rating:</h6>
              <div
                v-for="star in Math.round(show.vote_average / 2)"
                :key="star"
              >
                <font-awesome-icon icon="star" class="gold" />
              </div>
              <div
                v-for="star in 5 - Math.round(show.vote_average / 2)"
                :key="star"
              >
                <font-awesome-icon icon="star" class="gray" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Search from "./Search.vue";

export default {
  components: {
    Search,
  },

  data() {
    return {
      movies: [],
      shows: [],
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

      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=b8a9c9466f2868b183c2e2880382011d&query=${this.searchText}`
        )
        .then((r) => {
          this.shows = r.data.results;
        })
        .catch((error) => {
          console.log(error, "ERROR");
        });
    },
  },
};
</script>

<style lang="scss">
.card {
  height: 100%;
  background: rgb(20, 20, 20) !important;
}

.gold {
  color: gold;
}

.gray {
  color: lightgray;
}
</style>