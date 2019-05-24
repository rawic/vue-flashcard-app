<template>
  <div class="search-box">
    <svg
      class="searchicon"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      viewBox="0 0 17 17"
      version="1.1"
    >
      <g id="surface1">
        <path
          style=" stroke:none;fill-rule:nonzero;fill:rgb(0%,0%,0%);fill-opacity:1;"
          d="M 16.851562 16.132812 L 12.71875 12 C 13.828125 10.726562 14.5 9.066406 14.5 7.25 C 14.5 3.25 11.246094 0 7.25 0 C 3.25 0 0 3.253906 0 7.25 C 0 11.242188 3.253906 14.496094 7.25 14.496094 C 9.066406 14.496094 10.730469 13.824219 12.003906 12.71875 L 16.136719 16.847656 C 16.234375 16.945312 16.363281 17 16.492188 17 C 16.621094 17 16.753906 16.949219 16.851562 16.847656 C 17.046875 16.652344 17.046875 16.328125 16.851562 16.132812 Z M 1.015625 7.25 C 1.015625 3.8125 3.8125 1.019531 7.246094 1.019531 C 10.683594 1.019531 13.476562 3.816406 13.476562 7.25 C 13.476562 10.683594 10.683594 13.484375 7.246094 13.484375 C 3.8125 13.484375 1.015625 10.6875 1.015625 7.25 Z M 1.015625 7.25 "
        />
      </g>
    </svg>
    <input
      v-model="search"
      @keyup="searchCards"
      type="text"
      class="input"
      placeholder="Search"
    />
  </div>
  <!-- end of search box -->
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      search: this.search || ""
    };
  },
  methods: {
    searchCards() {
      this.$emit("searchTrigger", this.search);
    }
  }
};
</script>

<style scoped lang="sass">
@import 'src/assets/sass/_variables.sass';
.search-box
  background-color: $greybg
  width: 300px
  border-radius: $radius
  height: 40px
  display: flex
  align-items: center
  margin-left: auto
  margin-right: auto
  position: relative
  overflow: hidden
  transition: background-color .3s
  &:hover
    background-color: darken($greybg, 3%)

  .searchicon
    width: 17px
    position: absolute
    left: 15px

  .input
    border: none
    background-color: transparent
    height: 100%
    width: 100%
    padding-left: 42px
    padding-right: 15px
    border-radius: $radius
    transition: all .3s
    &:focus
      background-color: $highlight
      color: white
      &::placeholder
        color: white
</style>
