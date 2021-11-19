<template>
  <header>
    <div class="searchbox">
      <input
        @keyup.enter="$emit('search', searchString)"
        v-model="searchString"
        type="search"
        placeholder="Search a movie"
      />

      <button @click="$emit('search', searchString)">Search</button>
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