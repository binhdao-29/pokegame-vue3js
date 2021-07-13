<template>
  <div>
    <main-screen v-if="status === 'main'" @onStart="beforeStart($event)" />
    <interact-screen
      v-if="status === 'match'"
      :cardsContext="settings.cardsContext"
      :backgroundImg="this.backgroundImg"
      @onFinish="getResult"
    />
    <result-screen
      v-if="status === 'result'"
      :timer="settings.timer"
      @onStartAgain="status = 'main'"
    />
  </div>
</template>

<script>
import MainScreen from "./components/Main.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffled } from "./utils/array.js";

export default {
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data() {
    return {
      status: "main",
      settings: {
        cardsContext: [],
        timeStart: 0,
        timer: 0,
      },
      backgroundImg: "",
    };
  },
  methods: {
    beforeStart(sizeBlock) {
      this.backgroundImg = sizeBlock.sizeBlock;
      let totalCard = 0;

      // amount card render when user chose
      switch (sizeBlock.sizeBlock) {
        case "4x4":
          totalCard = 16;
          break;
        case "6x6":
          totalCard = 36;
          break;
        case "8x8":
          totalCard = 64;
          break;
        case "10x10":
          totalCard = 100;
          break;
      }

      const listCard = Array.from({ length: totalCard / 2 }, (_, i) => i + 1);
      const cards = [...listCard, ...listCard];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      this.settings.timeStart = new Date().getTime();

      this.status = "match";
    },
    getResult() {
      // get timer
      this.settings.timer = new Date().getTime() - this.settings.timeStart;

      // switch to result screen
      this.status = "result";
    },
  },
};
</script>

<style></style>
