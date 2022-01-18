<template>
  <header>
    <div class="header">
      <SearchBar v-if="query === ''" />
      <div v-if="query !== ''" class="header_query">
        <h2>
          Search Results for <span>"{{ query }}"</span>
        </h2>
        <button @click="clearQuery" class="header_query_icon">
          <i class="fas fa-times"></i>
        </button>
      </div>
    </div>
  </header>
</template>

<script>
import SearchBar from "@/components/SearchBar.vue";
import { mapGetters } from "vuex";

export default {
  name: "Header",
  components: {
    SearchBar,
  },
  computed: mapGetters(["query"]),
  methods: {
    async clearQuery() {
      await this.$store.dispatch("updateQuery", "");
    },
  },
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.header {
  background: $secondary-color;
  height: 400px;
  width: 100%;
  padding: 1.5em;
  @include flex;

  &_query {
    width: 100%;
    max-width: 1000px;
    margin: auto;
    @include flex($justify: space-between, $wrap: nowrap );

    h2 {
      font-size: 1.6rem;

      span {
        color: $grey-color;
        text-transform: capitalize;
      }
    }

    &_icon {
      font-size: 1.2rem;
      background: none;
      border: none;
      outline: none;
      cursor: pointer;
      margin-left: 8px;
    }
  }
}
</style>
