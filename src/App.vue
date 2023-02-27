<template>
  <MainScreen v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart" />
  <InteractScreen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onfinish="onGetResult"
  />
  <ResultScreen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="onStartAgain"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffled } from "./assets/utils/array";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
        timer: 0,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(value) {
      // this.settings.totalOfBlocks = value;
      const firstCards = Array.from(
        {
          length: value / 2,
        },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const card = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(shuffled(card));
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
    },
    onStartAgain() {
      this.statusMatch = "default";
    },
  },
};
</script>

<style></style>
