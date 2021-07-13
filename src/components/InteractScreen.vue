<template>
  <div class="interact-container" :class="`background-${backgroundImg}`">
    <div class="interact-wrapper">
      <card-item
        v-for="(card, index) in cardsContext"
        :key="index"
        :card="{ index: index, value: card }"
        @onFlip="checkRule($event)"
        :ref="`card-${index}`"
      />
    </div>
  </div>
</template>

<script>
import CardItem from "./CardItem.vue";

export default {
  data() {
    return {
      rules: [],
    };
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
    backgroundImg: String,
  },
  components: {
    CardItem,
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) {
        return false;
      }

      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.rules = [];

        //check amount flip card
        const amounFlipCard = document.querySelectorAll(
          ".card .card__inner.on-flip"
        );
        if (amounFlipCard.length === this.cardsContext.length - 1) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 1000);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          // close two card
          this.$refs[`card-${this.rules[0].index}`].onBackCard();
          this.$refs[`card-${this.rules[1].index}`].onBackCard();

          //reset rules
          this.rules = [];
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>

<style lang="scss">
.interact-container {
  display: flex;
  justify-content: center;
  align-items: center;

  background-position: center;
  background-size: cover;

  width: 100%;
  height: 100%;

  padding: 6rem 0;
}

.interact-wrapper {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;

  max-width: 22.4rem;

  margin-top: 2rem;

  @media screen and (min-width: 576px) {
    max-width: 30.4rem;
  }

  @media screen and (min-width: 768px) {
    max-width: 42.4rem;
  }
}

.background-4x4 {
  background-image: linear-gradient(
      0deg,
      rgba(0, 27, 36, 0.5) 0%,
      rgba(0, 0, 0, 0.5) 0%,
      rgba(0, 0, 0, 0.2) 100%
    ),
    url("../assets/images/easy.jpg");
}

.background-6x6 {
  background-image: linear-gradient(
      0deg,
      rgba(0, 27, 36, 0.5) 0%,
      rgba(0, 0, 0, 0.5) 0%,
      rgba(0, 0, 0, 0.2) 100%
    ),
    url("../assets/images/normal.jpg");
}

.background-8x8 {
  background-image: linear-gradient(
      0deg,
      rgba(0, 27, 36, 0.5) 0%,
      rgba(0, 0, 0, 0.5) 0%,
      rgba(0, 0, 0, 0.2) 100%
    ),
    url("../assets/images/hard.jpg");
}

.background-10x10 {
  background-image: linear-gradient(
      0deg,
      rgba(0, 27, 36, 0.5) 0%,
      rgba(0, 0, 0, 0.5) 0%,
      rgba(0, 0, 0, 0.2) 100%
    ),
    url("../assets/images/sp_hard.jpg");
}
</style>
