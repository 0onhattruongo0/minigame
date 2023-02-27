<template>
  <div class="scre">
    <h1>Interact Component here ...</h1>
    <Card
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{ index: index, value: card }"
      @onFlipped="onFlipped"
    />
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    Card,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    onFlipped(value) {
      console.log(this.rules);
      if (this.rules.length === 2) return false;
      this.rules.push(value);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("Right...");
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        // this.$refs[`card-${this.rules[0].index}`].onFlipBackCard();
        // this.$refs[`card-${this.rules[1].index}`].onFlipBackCard();
        console.log(this.$refs[`card-${this.rules[0].index}`].onFlipBackCard());
        this.rules = [];
      } else return false;
    },
  },
};
</script>
