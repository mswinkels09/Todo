<template>
  <div>
    <h1>ToDo List</h1>
    <p>{{itemsRemainedMessage}}</p>
    <div v-for="item in todos" :key="item.id">
      <TodoItem :todo="item" @status_change="handleStatusChange"/>
    </div>
  </div>
</template>

<script>
import { todoItems } from "../data";
import TodoItem from "./TodoItem";

export default {
  components: { TodoItem },
  data() {
    return {
      todos: [...todoItems]
    };
  },
  methods: {
    handleStatusChange(item) {
      item.complete = !item.complete
    }
  },
  computed: {
    itemsRemainedMessage() {
      const remaining = this.todos.filter(t => !t.complete).length;
      if (remaining == 1) {
        return "There is only 1 item left to do today!"
      }
      return `There are ${remaining} items left to do today!`
    }
  }
};
</script>

<style>
div {
  text-align: center;
}
  </style>
