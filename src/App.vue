<template>
  <div class="app">
    <div v-for="item of stopwatchCounter" :key="item">
      <Stopwatch />
    </div>
    <div class="block" style="cursor: pointer" @click="addStopwatch">
      <img class="add" src="src/assets/plus.svg" alt="plus">
    </div>
  </div>
</template>

<script>
import Stopwatch from "@/components/Stopwatch.vue";
export default {
  data() {
    return {
      stopwatchCounter : 0,
    }
  },
  methods: {
    addStopwatch() {
      this.stopwatchCounter++
    }
  },
  components : {
    Stopwatch
  }
};
</script>

<style >
.block {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #605c5c;
  border-radius: 8px;
  min-width: 320px;
  height: 160px;
  margin: 10px;
}
.app {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
}

ul {
  list-style: none;
}

.add {
  display: block;
  margin: auto;
  width: 60px;
  filter: invert(70%) sepia(0%) saturate(1156%) hue-rotate(176deg) brightness(91%) contrast(89%);
}
</style>