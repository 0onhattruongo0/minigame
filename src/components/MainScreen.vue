<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h2>Select mode to start game</h2>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(value) {
      this.$emit("onStart", value);
    },
  },
};
</script>
<style scoped>
.screen {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}
.screen button {
  padding: 1rem;
  background-color: var(--dark);
  color: var(--light);
  margin: 0.2rem;
  border-radius: 5px;
  cursor: pointer;
}
</style>
