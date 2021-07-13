<template>
  <div class="main-container">
    <div class="heading">POKE MEMORIES</div>
    <div class="subheading">Select mode to start game</div>

    <div class="main-content">
      <button
        class="btn"
        v-for="(content, index) in contents"
        :key="index"
        @click="onStart(content.size)"
      >
        <span>{{ content.size }}</span>
        <span>{{ content.level }}</span>
      </button>
    </div>

    <Footer />
  </div>
</template>

<script>
import Footer from "./Footer.vue";

export default {
  components: {
    Footer,
  },
  data() {
    return {
      contents: [
        { size: "4x4", level: "Easy" },
        { size: "6x6", level: "Normal" },
        { size: "8x8", level: "Hard" },
        { size: "10x10", level: "Super Hard" },
      ],
    };
  },
  methods: {
    onStart(sizeBlock) {
      this.$emit("onStart", { sizeBlock });
    },
  },
};
</script>

<style lang="scss">
.main-container {
  width: 100%;
  height: 100%;
  padding: 5rem 0 3rem;

  @media screen and (min-width: 576px) {
    height: 100vh;
  }

  background-image: linear-gradient(
      0deg,
      rgba(0, 27, 36, 1) 0%,
      rgba(0, 0, 0, 1) 0%,
      rgba(0, 0, 0, 0.42930675688244047) 100%
    ),
    url("../assets/images/bg.jpg");
  background-position: center;
  background-size: cover;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;

  color: var(--light);
  font-weight: 700;
  letter-spacing: 0.2rem;
}

.main-content {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 1rem;

  .btn {
    width: 10rem;
    height: 10rem;
    background: transparent;
    border: 1px solid var(--light);
    border-radius: 1rem;
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

    span {
      display: block;
    }
  }
}
</style>
