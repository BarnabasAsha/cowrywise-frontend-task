<template>
  <Header />
  <Loader v-if="loading" />
  <Gallery :photos="allPhotos" />
  <ImageModal
    v-if="Object.keys(activePhoto).length"
    :src="activePhoto.urls.regular"
    :author="activePhoto.user.name"
    :location="activePhoto.user.location"
  />
  <Error v-if="!loading && allPhotos.length <= 0" />
</template>

<script>
import Header from "@/components/Header.vue";
import Gallery from "@/components/Gallery.vue";
import ImageModal from "@/components/ImageModal.vue";
import Loader from "@/components/Loader.vue";
import Error from "@/components/Error.vue";
import { mapGetters } from "vuex";

export default {
  name: "App",
  components: {
    Header,
    Gallery,
    ImageModal,
    Loader,
    Error,
  },
  computed: mapGetters(["allPhotos", "loading", "query", "activePhoto"]),
  created() {
    this.initPhotos();
  },
  methods: {
    async initPhotos() {
      try {
        await this.$store.dispatch("fetchPhotos", {
          query: "African",
          order_by: "latest",
          per_page: 12,
        });
      } catch (error) {
        console.log(error.response.data);
      }
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap");
@import "./styles/mixins.scss";

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Inter", sans-serif;
  background: $primary-color;
}

img {
  width: 100%;
  height: 100%;
}
</style>
