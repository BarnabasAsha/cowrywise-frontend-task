<template>
  <div class="modal_wrapper">
    <figure class="modal">
      <div class="modal_image">
        <img :src="src" alt="" />
      </div>
      <figcaption class="modal_caption">
        <div class="modal_caption_author">{{ author }}</div>
        <div class="modal_caption_location">{{ location }}</div>
      </figcaption>
    </figure>
    <button @click="closeModal" class="close_icon">
      <i class="fas fa-times"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "ImageModal",
  props: {
    src: {
      type: String,
      required: true,
    },
    author: String,
    location: String,
  },
  methods: {
    async closeModal() {
      await this.$store.dispatch("setActivePhoto", {});
    },
  },
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.modal_wrapper {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 200;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.26);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1em;

  .close_icon {
    font-size: 1.5rem;
    color: $primary-color;
    position: absolute;
    top: 20px;
    right: 20px;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
  }

  .modal {
    width: 100%;
    max-width: 1000px;
    margin: auto;
    height: 90%;
    background: $primary-color;
    border-radius: 10px;
    overflow: hidden;
    @include flex($direction: column);
    animation: fadeUp 1000ms;
    transition: all ease-in 0.5s;

    &_image {
      width: 100%;
      height: 85%;
      @include flex;

      img {
        height: auto;
        width: auto;
        max-width: 100%;
        max-height: 100%;
        object-fit: cover;
      }
    }

    &_caption {
      height: 15%;
      background: $primary-color;
      width: 100%;
      padding: 1.5em 2em;
      @include flex($direction: column, $align: start, $wrap: nowrap);

      &_author {
        font-size: 1.1rem;
        line-height: 1.5rem;
        font-weight: bold;
      }

      &_location {
        font-size: 1rem;
        text-transform: capitalize;
        color: $grey-color;
      }
    }
  }

  @keyframes fadeUp {
    from {
      transform: translateY(50%);
    }
    to {
      transform: translateY(0);
    }
  }
}
</style>
