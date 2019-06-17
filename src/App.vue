<template>
  <div id="app">
    <Header/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" v-on:completed="completed"/>
    <AddTodo v-on:add-todo="addTodo"/>
  </div>
</template>

<script>
import Header from "./components/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import axios from 'axios';

export default {
  name: "App",
  components: {
    AddTodo,
    Header,
    Todos
  },
  data() {
    return {
      todos: [
        // {
        //   id: 1,
        //   title: "beach",
        //   completed: false
        // },
        // {
        //   id: 2,
        //   title: "subway",
        //   completed: true
        // },
        // {
        //   id: 3,
        //   title: "Internet",
        //   completed: false
        // }
      ]
    };
  },
  methods: {
    deleteTodo(_id) {
      var id = _id
      axios.delete('http://localhost:8081/posts/' + id)
        .then(res => this.todos = this.todos.filter(todo => todo._id !== _id))
        .catch(err => console.log(err));
      ;
      
    },

    
    completed(_id){
      var id = _id
      axios.put('http://localhost:8081/posts/put/'+id)
        .then(res => console.log("updated"))
        .catch(err=>console.log(err))
    },

    addTodo(newTodo){
      const { title, completed } = newTodo
      axios.post('http://localhost:8081/posts',{
        title,
        completed
      })
        .then(res => this.todos = [...this.todos,res.data])
        //.then(console.log(res.data))
        .catch(err => console.log(err));
      
    }
  },
    created(){
      axios.get('http://localhost:8081/posts')
        .then(res => this.todos = res.data)
        .catch(err => console.log(err));


    
  }
  
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
