
<template>
  <header class="AddTodo">
    <form @submit="addTodo">
      <!-- <input type="text" v-model="title" name="title" placeholder="Add Todo ..."> -->
      <div class="button">
        <md-field>
          <label>Add Todo ...</label>
          <md-input type="text" v-model="title" name="title"></md-input>
        </md-field>
      </div>
      <!-- <input type="submit" vulue="submit" class="md-primary"> -->
      <md-button type="submit" vulue="submit" class="add md-raised md-primary">Add</md-button>
    </form>
  </header>
</template>

<script>
// import uuid from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        // id: uuid.v4(),
        title: this.title,
        completed: false
      };

      //send to parent
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style scoped>
.button {
  width: 40%;
  margin: auto;
}
.add {
  margin-top: 20px;
}
</style>
