<template>
  <div v-bind:class="{'isCompleted':todo.completed}">
    <p class="font">
      <!-- <input type="checkbox" v-on:change="markComplete"> -->
      <md-checkbox type="checkbox" v-on:change="markComplete" v-model="this.todo.completed" @change="$emit('completed', todo._id)"></md-checkbox>
      {{todo.title}}
      <!-- <button class="del" @click="$emit('del-todo', todo.id)">X</button> -->
      <md-button @click="$emit('del-todo', todo._id)" class="small md-fab md-mini md-plain">
        <md-icon class='minus'></md-icon>
      </md-button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      console.log(this.todo.completed)
      //send to db
      // this.$emit("completed", this.todo.completed);
    }
}
}
</script>

<style scoped>
.isCompleted {
  text-decoration: line-through;
}
.del {
  background-color: rgb(201, 11, 11);
  border-width: 0;
  color: whitesmoke;
  border-radius: 20px;
  padding: 5 px;
}

.small {
  width: 50%;
  height: 50%;
transform: scale(0.3)
  /*padding: auto;*/
}

.minus{
  margin-bottom: 3px;
}

.font{
  font-size: 1.5em;
}
</style>


