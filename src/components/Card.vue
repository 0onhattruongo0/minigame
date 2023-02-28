<template>
  <div
    class="card"
    :class="{ disable: isDisable }"
    :style="{
      // height: `${(920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      height: `${
        98 / Math.sqrt(cardsContext.length) -
        98 / Math.sqrt(cardsContext.length) / 10
      }vh`,
      width: `${
        ((98 / Math.sqrt(cardsContext.length) -
          98 / Math.sqrt(cardsContext.length) / 10) *
          3) /
        4
      }vh`,
      marginRight: `${98 / Math.sqrt(cardsContext.length) / 50}vh`,
      marginBottom: `${98 / Math.sqrt(cardsContext.length) / 50}vh`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-flipped': is_flipped }"
      @click="onToggleFlipCard"
    >
      <div
        class="card__face card__face--front"
        :style="{
          padding: `${98 / Math.sqrt(cardsContext.length) / 12}vh`,
        }"
      >
        <div class="card__content"></div>
      </div>
      <div
        class="card__face card__face--back"
        :style="{
          padding: `${98 / Math.sqrt(cardsContext.length) / 12}vh`,
        }"
      >
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
      required: true,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isDisable: false,
      is_flipped: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisable) {
        return false;
      }
      this.is_flipped = !this.is_flipped;
      if (this.is_flipped) this.$emit("onFlipped", this.card);
    },
    onFlipBackCard() {
      this.is_flipped = false;
    },
    onEnableDisableMod() {
      this.isDisable = true;
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  display: inline-block;
  width: 90px;
  height: 120px;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card.disable .card__inner {
  cursor: default;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card__face--back .card__content {
  height: 100%;
  background-size: 100%;
  background-repeat: no-repeat;
  background-position: center center;
}
.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 100%;
  height: 100%;
  width: 100%;
}
</style>
