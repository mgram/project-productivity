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
        <Timer
          :count="getCount"
          :key="getCount"
          @onCompletion="(value) => addCompletion(value)"
        />
      </div>
      <div class="completions">
        <h1 class="totalTime">
          <span>{{ getTotalTime }} </span>
        </h1>
        <ul>
          <li
            v-for="completion in completedItems"
            :key="completion.id"
            class="completionItem"
          >
            Completed a work session at {{ completion.endTime }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "IndexPage",
  data() {
    return {
      mode: "work",
      completedItems: [],
    };
  },
  mounted() {
    if (localStorage.completions) {
      this.completedItems = JSON.parse(localStorage.completions);
    }
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
    getTotalTime() {
      return this.completedItems.length * 20 + " mins";
    },
  },
  methods: {
    resetTodos() {
      if (localStorage) {
        localStorage.removeItem("todos");
        localStorage.removeItem("completions");
        this.completedItems = [];
        this.$refs.list.clearTodos();
      }
    },
    setWork() {
      this.mode = "work";
    },
    setBreak() {
      this.mode = "break";
    },
    addCompletion(value) {
      if (this.mode == "work") {
        value.id = uuidv4();
        this.completedItems.push(value);
        if (localStorage) {
          localStorage.removeItem("completions");
          localStorage.completions = JSON.stringify(this.completedItems);
        }
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
  width: 60%;
}
.timer {
  font-size: 12px;
  margin: 20px;
  padding: 20px;
  margin-top: 0px;
}
.completions {
  font-size: 12px;
  text-align: center;
  margin: 20px;
  padding: 20px;
  display: flex;
  flex-direction: column;
}
.completionItem {
  text-align: left;
  font-size: 20px;
  line-height: 1.5;
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
  position: absolute;
  right: 50px;
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
.totalTime {
  text-align: left;
  font-size: 32px;
}
span {
  color: green;
}
</style>
