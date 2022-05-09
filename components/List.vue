<template>
  <div ref="items">
    <div v-for="(item, index) in items" :key="item.id">
      <Item
        :text="item.todo"
        :itemStatus="item.status"
        :index="index"
        @insertTodo="(index) => insertItem(index)"
        @removeTodo="(index) => removeItem(index)"
        @handleKey="(index, keyType) => handleKey(index, keyType)"
        @statusChanged="(index, status) => updateStatus(index, status)"
        @textChanged="(index, text) => updateText(index, text)"
        :id="item.id"
      />
    </div>
  </div>
</template>

<script>
import Item from "./Item.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  mounted() {
    if (localStorage.todos) this.items = JSON.parse(localStorage.todos);
  },
  data() {
    return {
      items: [
        {
          id: uuidv4(),
          todo: "",
          status: "active",
        },
      ],
    };
  },
  methods: {
    insertItem(index) {
      let itemToInsert = {
        id: uuidv4(),
        todo: "",
        status: "active",
      };
      this.items.splice(index + 1, 0, itemToInsert);
      this.moveFocus(index + 1);
      this.save();
    },
    removeItem(index) {
      if (this.items.length == 1) return;
      this.items.splice(index, 1);
      this.moveFocus(index - 1);
      this.save();
    },
    handleKey(index, keyType) {
      if (keyType == "up") {
        if (index != 0) this.moveFocus(index - 1);
      }
      if (keyType == "down") {
        if (index != this.items.length - 1) this.moveFocus(index + 1);
      }
    },
    moveFocus(index) {
      this.$nextTick(() => {
        this.$refs.items.children[index].querySelector("input").focus();
      });
    },
    updateStatus(index, status) {
      this.items[index].status = status;
      this.save();
    },
    updateText(index, text) {
      this.items[index].todo = text;
      this.save();
    },
    save() {
      if (localStorage) {
        localStorage.todos = JSON.stringify(this.items);
      }
    },
  },
};
</script>

<style>
</style>