<template>
  <div class="item">
    <div class="action" @click="toggle" :class="{ fill: isDone() }"></div>
    <input
      v-model="todo"
      type="text"
      class="text"
      :class="{ done: isDone() }"
      @keyup.enter="handleEnter(index)"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      status: this.itemStatus,
      todo: this.text,
    };
  },
  props: ["text", "itemStatus", "index", "id"],
  methods: {
    toggle() {
      if (this.status == "active") {
        this.status = "done";
      } else if (this.status == "done") {
        this.status = "active";
      }
    },
    isDone() {
      return this.status == "done";
    },
    handleEnter(index) {
      this.$emit("insertTodo", index);
    },
  },
};
</script>

<style>
.item {
  display: flex;
  margin-bottom: 15px;
}
.action {
  border-radius: 50%;
  height: 20px;
  width: 20px;
  margin-right: 10px;
  border: lightblue 1px solid;
}
.text {
  border-radius: 2px;
  font-size: 18px;
  border: 0px none;
  -webkit-appearance: none;
  width: 80%;
}
.text:focus {
  outline: none;
  border-bottom: lightblue 1px solid;
}
.done {
  text-decoration: line-through;
}
.fill {
  background: lightblue;
}
</style>