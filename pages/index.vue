<template>
  <div class="container">
    <div class="todos">
      <div class="label">
        <h1>Today's tasks</h1>
        <div class="reset" @click="resetTodos"></div>
      </div>
      <List ref="list" />
    </div>
    <div class="pomodoro">
      <div class="selections">
        <p :class="workClass" @click="setWork">Work</p>
        <p :class="breakClass" @click="setBreak">Break</p>
      </div>
      <div class="timer">
        <Timer :count="getCount" :key="getCount" />
      </div>
      <div class="completions">
        <h1>Completions go here</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      mode: "work",
    };
  },
  computed: {
    workClass() {
      if (this.mode == "work") return "pill active";
      else return "pill";
    },
    breakClass() {
      if (this.mode == "break") return "pill active";
      else return "pill";
    },
    getCount() {
      if (this.mode == "work") return 1200;
      if (this.mode == "break") return 600;
    },
  },
  methods: {
    resetTodos() {
      if (localStorage) {
        localStorage.removeItem("todos");
        this.$refs.list.clearTodos();
      }
    },
    setWork() {
      this.mode = "work";
    },
    setBreak() {
      this.mode = "break";
    },
  },
};
</script>
<style scoped>
.container {
  display: flex;
  flex-direction: row;
  width: 100%;
}
.todos {
  width: 40%;
  margin: 20px;
  text-align: center;
  padding: 20px;
  font-size: 12px;
}
.pomodoro {
  display: flex;
  flex-direction: column;
  width: 60%;
}
.timer {
  font-size: 12px;
  margin: 20px;
  padding: 20px;
  margin-top: 0px;
}
.completions {
  background: grey;
  font-size: 12px;
  text-align: center;
  margin: 20px;
  padding: 20px;
}
.todos h1 {
  text-align: left;
  margin-bottom: 20px;
}
.label {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.reset {
  background: lightpink;
  height: 10px;
  width: 10px;
  color: whitesmoke;
  text-align: center;
  border-radius: 50%;
  align-self: center;
  position: relative;
}
.reset:hover {
  background: red;
  cursor: pointer;
}
.selections {
  display: flex;
  flex-direction: row;
  justify-content: left;
  width: 60%;
  margin-bottom: 0;
  margin-top: 30px;
  margin-left: 40px;
}
.pill {
  background: grey;
  padding: 10px 20px 10px 20px;
  color: whitesmoke;
  border-radius: 40%;
  font-size: 18px;
  margin-right: 20px;
}
.pill:hover {
  cursor: pointer;
}
.pill.active {
  background: black;
}
</style>
