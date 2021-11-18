<template>
  <header>
    <div class="searchbox">
      <input
        v-model="searchString"
        type="search"
        placeholder="Search a movie"
      />

      <button @click="$emit('search-movie', searchString)">Search</button>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      searchString: "",
    };
  },
};
</script>

<style>
</style>