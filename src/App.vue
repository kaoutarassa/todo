<template>
<div id="app">
  <h1> TODO List</h1>
  <input v-model="todoName" @keyup.enter="addTodo" type="text"/>
  <ul>
    <li v-for="todo of todos" :key="todo.id">
        {{todo.name}}
    </li>
    
  </ul>
</div> 
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  baseUrl : "http://localhost:3000/todos",
  data() {
    return{
      todos: [],
      todoName: ''
    }
  },
  methods:{
    async Created(){
      try {
        const result= await axios.get("http://localhost:3000/todos");
        this.todos = result.data;
        console.log(this.todos)
        } catch(e){
          console.error(e)
        }
    },
    async addTodo(){
      const result = await axios.post("http://localhost:3000/todos", { name: this.todoName })

      this.todos = [...this.todos, result.data]

      this.todoName = ''
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

li {
  list-style: none;
}

h1 {
  color: #a29bfe
}
</style>
