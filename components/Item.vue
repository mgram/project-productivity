<template>
  <div class="item">
    <div class="action" @click="toggle" :class="{ fill: isDone() }"></div>
    <input
      v-model="todo"
      type="text"
      class="text"
      :class="{ done: isDone() }"
      @keyup.enter="handleEnter(index)"
      @keydown.delete="handleDelete(index)"
      @keyup.up="handleUp(index)"
      @keyup.down="handleDown(index)"
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
  watch: {
    status: function () {
      this.$emit("statusChanged", this.index, this.status);
    },
    todo: function () {
      this.$emit("textChanged", this.index, this.todo);
    },
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
    handleDelete(index) {
      if (this.todo == "") this.$emit("removeTodo", index);
    },
    handleUp(index) {
      this.$emit("handleKey", index, "up");
    },
    handleDown(index) {
      this.$emit("handleKey", index, "down");
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