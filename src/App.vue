<template>
  <div id="app">
    <SiteHeader :searchString="searchText" @search="search" />
    <SiteMain :moviesMain="moviesApp" :showsMain="showsApp" />
  </div>
</template>

<script>
import SiteMain from "./components/SiteMain.vue";
import SiteHeader from "./components/SiteHeader.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    SiteMain,
    SiteHeader,
  },

  data() {
    return {
      moviesApp: [],
      showsApp: [],
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
          this.moviesApp = r.data.results;
        })
        .catch((error) => {
          console.log(error, "ERROR");
        });

      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=b8a9c9466f2868b183c2e2880382011d&query=${this.searchText}`
        )
        .then((r) => {
          this.showsApp = r.data.results;
        })
        .catch((error) => {
          console.log(error, "ERROR");
        });
    },
  },
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";
body {
  background: rgb(70, 70, 70);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
