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
      <div class="timer">
        <h1>Timer goes here</h1>
      </div>
      <div class="completions">
        <h1>Completions go here</h1>
      </div>
    </div>
  </div>
</template>

<script>
import List from "../components/List.vue";
export default {
  name: "IndexPage",
  components: {
    List,
  },
  methods: {
    resetTodos() {
      if (localStorage) {
        localStorage.removeItem("todos");
        this.$refs.list.clearTodos();
      }
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
  width: 100%;
}
.timer {
  background: grey;
  font-size: 12px;
  text-align: center;
  margin: 20px;
  padding: 20px;
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
</style>
