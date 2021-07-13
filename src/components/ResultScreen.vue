<template>
  <div class="result-container">
    <div class="heading">✨ Congratulations ✨</div>
    <div class="subheading">{{ Math.round(timer / 1000) }} seconds</div>
    <button class="btn-play" @click="onStartAgain">Play again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      require: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>

<style lang="scss">
.result-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  width: 100%;
  height: 100vh;

  background: rgb(131, 58, 180);
  background: linear-gradient(
    90deg,
    rgba(131, 58, 180, 1) 0%,
    rgba(253, 29, 29, 0.4433123591233369) 50%,
    rgba(252, 176, 69, 1) 100%
  );

  .btn-play {
    width: 8rem;
    height: 3rem;
    background-color: var(--dark);
    border: 1px solid var(--dark);
    border-radius: 0.7rem;
    margin: 0.8rem;
    text-align: center;

    color: var(--light);
    font-family: var(--text-font);
    font-size: 1.5rem;

    transition: all 0.35s;

    cursor: pointer;

    &:hover {
      color: var(--dark);
      background-color: var(--light);
    }
  }

  .heading {
    font-size: 2.5rem;

    @media screen and (min-width: 576px) {
      font-size: 4rem;
    }
  }
}
</style>
