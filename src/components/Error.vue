<template>
  <div class="error">
    <div class="error_img">
      <img src="../assets/oops.png" alt="" />
    </div>
    <h3>Something Occured</h3>
    <p>
      Seems we can't find what you are looking for <br />
      Please try again
    </p>
  </div>
</template>

<script>
export default {
  name: "Error",
};
</script>

<style lang="scss">
@import "../styles/mixins.scss";

.error {
  width: 100%;
  height: 300px;
  @include flex($direction: column);

  .error_img {
    width: 100%;
    max-width: 300px;
  }

  h3 {
    font-size: 1.4rem;
    line-height: 2rem;
    text-align: center;
    margin-bottom: 10px;
  }

  p {
    font-size: 1.1rem;
    text-align: center;
  }
}
</style>
