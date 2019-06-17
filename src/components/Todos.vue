<template>
  <div>
    <div v-bind:key="todo._id" v-for="todo in todos">
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo._id)" v-on:completed="$emit('completed', todo._id)"/>
    </div>
  </div>
</template>


<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos"]
};
</script>

<style scoped>
</style>
