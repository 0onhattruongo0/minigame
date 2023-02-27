<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart(value)"
  />
  <InteractScreen v-if="statusMatch === 'match'" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
  },
  data() {
    return {
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart() {
      this.statusMatch = "match";
    },
  },
};
</script>

<style></style>
