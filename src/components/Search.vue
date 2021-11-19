<template>
  <div class="head m-0">
    <div class="searchbox">
      <input
        @keyup.enter="$emit('search', searchString)"
        v-model="searchString"
        type="search"
        placeholder="Search a movie"
      />

      <button @click="$emit('search', searchString)">Search</button>
    </div>
  </div>
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

<style lang="scss">
.head {
  height: 100px;
  background: rgb(20, 20, 20);
}
</style>