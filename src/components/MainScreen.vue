<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h2>Select mode to start game</h2>
    <div class="actions">
      <button>
        <span>4x4</span>
        <span @click="onStart(16)">Easy</span>
      </button>
      <button>
        <span>6x6</span>
        <span @click="onStart(36)">Normal</span>
      </button>
      <button>
        <span>8x8</span>
        <span @click="onStart(64)">Hard</span>
      </button>
      <button>
        <span>10x10</span>
        <span @click="onStart(100)">Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(value) {
      this.$emit("onStart", { value });
    },
  },
};
</script>
