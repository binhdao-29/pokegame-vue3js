<template>
  <div class="card" @click="(e) => !isFlip && onFlipCard()">
    <div class="card__inner" :class="{ 'on-flip': isFlip }">
      <div class="card__face card__face--front"></div>
      <div
        class="card__face card__face--back"
        :style="{
          backgroundImage: `url(${require('../assets/images/' +
            card.value +
            '.png')})`,
        }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    card: {
      type: [String, Number, Array, Object],
    },
  },
  data() {
    return {
      isFlip: false,
    };
  },
  methods: {
    onFlipCard() {
      this.isFlip = !this.isFlip;

      // if card open, check card
      if (this.isFlip) {
        this.$emit("onFlip", this.card);
      }
    },
    onBackCard() {
      this.isFlip = false;
    },
  },
};
</script>

<style lang="scss">
.card {
  display: inline-block;
  width: 4rem;
  height: 6rem;
  margin: 0.8rem;

  perspective: 20rem;

  @media screen and (min-width: 576px) {
    width: 6rem;
    height: 9rem;
  }

  @media screen and (min-width: 768px) {
    width: 9rem;
    height: 12rem;
  }
}

.card__inner {
  position: relative;

  width: 100%;
  height: 100%;
  cursor: pointer;

  perspective: 3rem;

  transform-style: preserve-3d;
  transition: transform 1s;
}

.card__inner.on-flip {
  transform: rotateY(-180deg);
  pointer-events: none;
}

.card__face {
  position: absolute;
  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  backface-visibility: hidden;
  overflow: hidden;

  border-radius: 1rem;
  padding: 1rem;

  box-shadow: 0 3px 10px 3px rgba($color: #000000, $alpha: 0.2);
}

.card__face--front {
  background: var(--dark) url("../assets/images/icon_back.png") no-repeat center;
  background-size: 40px;

  @media screen and (min-width: 576px) {
    background-size: 60px;
  }
}

.card__face--back {
  background-color: var(--light);
  background-position: center;
  background-size: 80%;
  background-repeat: no-repeat;
  transform: rotateY(-180deg);
}
</style>
