<template>
  <div class="search-container">
    <label>
      <input
        class="search-input"
        type="text"
        placeholder="Search"
        v-model="searchText"
      />
    </label>
    <button class="search-btn" @click="$emit('search', this.searchText)">
      <img class="search-icon" src="../assets/search-icon.png" />
    </button>
    <button v-if="searchText" @click="$emit('clear', this.searchText)">
      Скинути фільтер
    </button>
  </div>
</template>

<script>
export default {
  name: "SearchContactForm",

  data() {
    return {
      searchText: null,
    };
  },

  methods: {},
};
</script>

<style lang="css" scoped>
.search-container {
  position: relative;
}
.search-input {
  min-height: 30px;
  width: 100%;
  padding-right: 40px;
}
.search-btn {
  background: none;
  border: none;
  cursor: pointer;
  position: absolute;
  right: -35px;
  top: 2px;
}
.search-icon {
  width: 30px;
}
</style>