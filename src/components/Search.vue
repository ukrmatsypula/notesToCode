<template>
  <div class="wrapper-search">
    <div class="search">
      <input
        class="search-input"
        type="text"
        :placeholder="placeholder"
        v-model="search"
      />
      <div class="search-icon-wrap">
        <svg class="icon search-icon">
          <use xlink:href="../assets/sprite.svg#search"></use>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "search",
  props: {
    value: {
      type: String,
      requied: true,
    },
    placeholder: {
      type: String,
      default: "Search",
    },
  },
  data: () => ({
    search: "",
  }),
  watch: {
    search(val) {
      this.$emit("search", val);
    },
  },
};
</script>

<style lang="scss">
.search {
  position: relative;
}

.search-input {
  position: relative;
  margin-bottom: 0;
  padding-left: 50px;
  font-family: montserrat;
}
.search-icon {
  position: absolute;
  top: -46px;
  left: 13px;
  z-index: 1;
  fill: lightgrey !important;
}
</style>
