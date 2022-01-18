<template>
  <div class="loader">
    <div v-for="i in 6" :key="i" class="loader_box">
      <div class="loader_box_items">
        <span></span>
        <span></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Loader",
  mounted() {
    const loaders = document.getElementsByClassName("loader_box");
    loaders[1].classList.add("boxx");
    loaders[2].classList.add("boxx");
    loaders[5].classList.add("boxx");
  },
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.loader {
  width: 100%;
  max-width: 1000px;
  margin: auto;
  transform: translateY(-100px);
  padding: 1.5em;
  @include grid;

  .loader_box {
    position: relative;
    width: 300px;
    height: 300px;
    background: #e5e5e5;
    @include flex($justify: flex-end, $align: flex-start, $direction: column);
    border-radius: 12px;
    margin-bottom: 2rem;
    overflow: hidden;

    &::after {
      content: "";
      background-color: #e1e1e1;
      position: absolute;
      top: 0;
      bottom: 0;
      width: 100%;
      height: 100%;
      animation: 1.5s skeleton ease-out infinite;
      z-index: 10;
    }

    &.boxx {
      height: 360px;
    }

    &_items {
      position: relative;
      padding: 1em;
      z-index: 15;

      span {
        display: block;
        width: 50px;
        height: 10px;
        background: #c4c4c4;
        margin-bottom: 3px;
      }

      span:nth-child(1) {
        width: 50px;
      }
      span:nth-child(2) {
        width: 80px;
      }
    }
  }

  @keyframes skeleton {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }
}
</style>
