<template>
  <figure class="image">
    <img :src="src" alt="photo" />
    <figcaption class="image_caption">
      <div class="image_caption_author">{{ author }}</div>
      <div class="image_caption_location">{{ location }}</div>
    </figcaption>
  </figure>
</template>

<script>
export default {
  name: "Image",
  props: {
    src: {
      type: String,
      required: true,
    },
    author: String,
    location: String,
  },
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.image {
  position: relative;
  width: 100%;
  height: auto;
  border-radius: 12px;
  overflow: hidden;
  margin-bottom: 2rem;

  &_caption {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    z-index: 15;
    color: $primary-color;
    padding: 1em;
    opacity: 0;

    &_author {
      font-size: 1.1rem;
      line-height: 1.5rem;
      font-weight: 500;
    }

    &_location {
      font-size: 0.8rem;
      font-weight: 400;
      text-transform: capitalize;
    }
  }

  &:hover::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 99%;
    background: rgba(0, 0, 0, 0.534);
    z-index: 12;
    border-radius: 12px;
    cursor: zoom-in;
  }

  &:hover &_caption {
    opacity: 1;
  }
}
</style>
