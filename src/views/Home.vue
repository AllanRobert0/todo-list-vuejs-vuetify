<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos :todoList="todoList" v-on:del-todo="deleteTodo"/>
  </div>
</template> 

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";


export default {
  name: 'App',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todoList: []
    }
  },
  methods: {
    deleteTodo(id) {
      console.log(id)
      this.todoList = this.todoList.filter(todo => todo.id !== id)
    },
    addTodo(newTodo) {
      this.todoList = [newTodo, ...this.todoList]
    }
  }
}
</script>
