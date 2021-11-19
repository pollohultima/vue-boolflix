<template>
  <div class="head pe-5 d-flex align-items-center justify-content-between">
    <div class="logo ps-5">
      <img
        src="https://fontmeme.com/permalink/211119/f5c422282f53e11f43fdde71afc7dcbc.png"
        alt=""
      />
    </div>
    <div class="searchbar">
      <input
        @keyup.enter="$emit('search', searchString)"
        v-model="searchString"
        type="search"
        placeholder="Search a movie"
        class="p-0"
      />

      <button
        class="btn-secondary border-0 rounded-end p-1"
        @click="$emit('search', searchString)"
      >
        Search
      </button>
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
  input {
    height: 32px;
  }
}
</style>