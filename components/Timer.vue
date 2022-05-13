<template>
  <div class="timer-container">
    <div v-if="timerState == 'start'" class="start" @click="toggle">
      <h2>START</h2>
    </div>
    <div v-if="timerState == 'abort'" class="abort" @click="toggle">
      <h2>ABORT</h2>
    </div>
    <h1>{{ getMinutes }} : {{ getSeconds }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timerState: "start",
      timer: this.count,
      shouldContinue: true,
      timeOutID: "",
    };
  },
  computed: {
    getSeconds() {
      return (this.timer % 60).toLocaleString("en-US", {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });
    },
    getMinutes() {
      return Math.floor(this.timer / 60).toLocaleString("en-US", {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });
    },
  },
  props: ["count"],
  watch: {
    timer: {
      handler(value) {
        if (this.timer < 0) {
          this.timerState = "start";
          this.timer = this.count;
          this.shouldContinue = false;
        } else if (this.timer >= 0 && this.shouldContinue == true) {
          this.timeOutID = setTimeout(() => this.timer--, 1000);
        }
      },
    },
  },
  methods: {
    toggle() {
      if (this.timerState == "start") {
        this.timerState = "abort";
        this.timer--;
        this.shouldContinue = true;
      } else if (this.timerState == "abort") {
        clearTimeout(this.timeOutID);
        this.shouldContinue = false;
        this.timerState = "start";
        this.timer = this.count;
      }
    },
  },
};
</script>

<style>
.timer-container {
  width: 60%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  padding: 30px;
  font-size: 20px;
  border: 2px solid slategray;
  display: flex;
  justify-content: space-around;
}
.start {
  background: green;
  color: whitesmoke;
  padding: 10px 30px 10px 30px;
}
.start:hover {
  cursor: pointer;
}
.abort {
  background: red;
  color: whitesmoke;
  padding: 10px 30px 10px 30px;
}
.abort:hover {
  cursor: pointer;
}
</style>