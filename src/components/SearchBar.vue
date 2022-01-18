<template>
  <form @submit.prevent="getPhotos" class="searchBar">
    <span class="searchBar_icon">
      <i class="fas fa-search"></i>
    </span>
    <input
      type="search"
      name="search"
      id="search"
      v-model="query"
      placeholder="Search for photo"
    />
  </form>
</template>

<script>
export default {
  name: "SearchBar",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    async getPhotos() {
      if (this.query !== "") {
        try {
          await this.$store.dispatch("fetchPhotos", {
            query: this.query,
            order_by: "latest",
            per_page: 12,
          });
          await this.$store.dispatch("updateQuery", this.query);
        } catch (error) {
          console.log(error.response.data);
        }
      }
    },
  },
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.searchBar {
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
  background: $primary-color;
  border-radius: 6px;
  height: 55px;
  display: flex;
  align-items: center;
  padding: 1em;

  &_icon {
    font-size: 1.3rem;
    color: $grey-color;
    margin-right: 1.5rem;
  }

  input {
    border: none;
    background: none;
    outline: none;
    width: 100%;
    height: 100%;
    font-size: 1rem;

    &:focus,
    &:active {
      background: none;
    }

    &::placeholder {
      font-size: 1rem;
      font-weight: 500;
    }
  }
}
</style>
