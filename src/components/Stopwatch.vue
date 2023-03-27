<template>
  <div class="block" :class="{active : isRunning}">
    <div class="display">
      {{ displayHours }} : {{ displayMinutes }} : {{ displaySeconds }}
    </div>
    <div class="controls">
      <img class="play" src="src/assets/start.svg" v-if="!isRunning" @click="start" alt="start"/>
      <img style="padding: 5px" class="pause" src="src/assets/pause.svg" v-if="isRunning" @click="stop" alt="stop"/>
      <img style="height: 60px; padding: 20px" class="reset" src="src/assets/reset.svg" @click="reset" alt="reset"/>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      displayHours: '00',
      hours : 0,
      displayMinutes: '00',
      minutes : 0,
      displaySeconds: '00',
      seconds : 0,
      milliseconds : 0,
      intervalId: null,
      previousTime: null,
    };
  },
  methods: {
    start() {
      this.isRunning = true;
      this.previousTime = new Date();
      this.intervalId = setInterval(() => {
        const currentTime = new Date();
        const elapsedTime = currentTime - this.previousTime;
        this.milliseconds += elapsedTime;
        this.previousTime = currentTime;
        if (this.milliseconds >= 1000) {
          this.seconds++
          this.seconds < 10 ? this.displaySeconds = '0' + this.seconds : this.displaySeconds = this.seconds;
          this.milliseconds -= 1000;
        }
        if (this.seconds >= 60) {
          this.minutes++
          this.seconds = 0;
          this.minutes < 10 ? this.displayMinutes = '0' + this.minutes : this.displayMinutes = this.minutes;
          this.displaySeconds = '00'
        }
        if (this.minutes >= 60) {
          this.hours++;
          this.minutes = 0;
          this.hours < 10 ? this.displayHours = '0' + this.hours : this.displayHours = this.hours;
          this.displayMinutes = '00';
        }
      }, 10);
    },
    stop() {
      this.isRunning = false;
      clearInterval(this.intervalId);
    },
    reset() {
      this.isRunning = false;
      this.displayHours = '00';
      this.displayMinutes = '00';
      this.displaySeconds = '00';
      this.minutes = 0;
      this.seconds = 0;
      this.hours = 0;
      this.milliseconds = 0;
      clearInterval(this.intervalId);
    },
  },
};
</script>

<style scoped>
.active .display {
  color: white;
  border-bottom: solid 1px white;
}

.active img {
  filter: invert(100%) sepia(0%) saturate(24%) hue-rotate(325deg) brightness(104%) contrast(107%);
}
.display {
  font-size: 3rem;
  margin: 0.5rem;
  border-bottom: solid 1px #9E9E9E;
  width: 100%;
  display: flex;
  justify-content: center;
}

img {
  width: 60px;
  filter: invert(70%) sepia(0%) saturate(1156%) hue-rotate(176deg) brightness(91%) contrast(89%);
  cursor: pointer;
}
</style>