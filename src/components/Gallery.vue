<template>
  <section class="gallery">
    <Image
      v-for="photo in photos"
      :key="photo.id"
      :src="photo.urls.regular"
      :author="photo.user.name"
      :location="photo.user.location"
      @click="setActivePhoto(photo)"
    />
  </section>
</template>

<script>
import Image from "./Image.vue";

export default {
  name: "Gallery",
  components: {
    Image,
  },
  props: {
    photos: {
      type: Array,
      required: true,
    },
  },
  methods: {
    async setActivePhoto(photo) {
      await this.$store.dispatch("setActivePhoto", photo);
    },
  },
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.gallery {
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
  transform: translateY(-100px);
  padding: 1.5em;
  @include grid;
}
</style>
