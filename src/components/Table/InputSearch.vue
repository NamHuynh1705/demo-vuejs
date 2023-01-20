<template>
  <div class="input-group">
    <b-input-group class="mt-3">
      <b-form-input
        class="input-search"
        type="text"
        @change="onChangeSearch"
      ></b-form-input>
      <b-icon class="icon-search" icon="search" variant="black"></b-icon>
      <b-input-group-append>
        <b-button variant="info">Search</b-button>
      </b-input-group-append>
    </b-input-group>
  </div>
</template>

<script>
export default {
  name: "InputSearch",
  props: {
    searchText: String,
  },
  methods: {
    onChangeSearch(evt) {
      this.$emit("handleSearch", evt);
    },
  },
};
</script>

<style>
.input-group {
  width: 80%;
  margin-top: 40px;
  position: relative;
}
.input-search {
  width: 300px !important;
  flex: unset !important;
  padding-left: 40px;
  border-top-left-radius: 7px !important;
  border-bottom-left-radius: 7px !important;
}
.icon-search {
  font-size: 20px;
  position: absolute;
  top: 9.5px;
  left: 10px;
  z-index: 10;
}
</style>