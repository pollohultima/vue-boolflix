<template>
  <main>
    <MoviesList :movies="moviesMain" :shows="showsMain" />
  </main>
</template>

<script>
import MoviesList from "./MoviesList.vue";
export default {
  props: {
    moviesMain: Array,
    showsMain: Array,
  },

  components: {
    MoviesList,
  },
};
</script>

<style>
</style>