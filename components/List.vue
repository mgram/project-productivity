<template>
  <div ref="items">
    <div v-for="(item, index) in items" :key="item.id">
      <Item
        :text="item.todo"
        :itemStatus="item.status"
        :index="index"
        @insertTodo="(index) => insertItem(index)"
        @removeTodo="(index) => removeItem(index)"
        :id="item.id"
      />
    </div>
  </div>
</template>

<script>
import Item from "./Item.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  data() {
    return {
      items: [
        {
          id: uuidv4(),
          todo: "Type a todo & press Enter",
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
    },
    removeItem(index) {
      if (this.items.length == 1) return;
      this.items.splice(index, 1);
      this.moveFocus(index - 1);
    },
    moveFocus(index) {
      this.$nextTick(() => {
        this.$refs.items.children[index].querySelector("input").focus();
      });
    },
  },
};
</script>

<style>
</style>