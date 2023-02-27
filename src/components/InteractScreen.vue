<template>
  <div class="screen">
    <div class="screen__inner">
      <Card
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        @onFlipped="onFlipped"
      />
    </div>
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
      this.rules.push(value);
      if (
        this.rules.length === 2 &&
        this.$refs[`card-${this.rules[0].index}`] ===
          this.$refs[`card-${this.rules[1].index}`]
      ) {
        this.rules.pop();
      }
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMod();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMod();
        this.rules = [];
        const disabledElement = document.querySelectorAll(
          ".screen .card.disable"
        );
        if (disabledElement.length === this.cardsContext.length - 2) {
          setTimeout(() => {
            this.$emit("onfinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
