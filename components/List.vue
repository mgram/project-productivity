<template>
  <div>
    <div v-for="(item, index) in items" :key="item.id">
      <Item
        :text="item.todo"
        :itemStatus="item.status"
        :index="index"
        @insertTodo="(index) => insertItem(index)"
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
          todo: "Sample todo 1",
          status: "active",
        },
        {
          id: uuidv4(),
          todo: "Sample todo 2",
          status: "done",
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
    },
  },
};
</script>

<style>
</style>