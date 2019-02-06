<template>
  <div id="app">
    <AddTodo
      v-on:add-todo="addTodo"
    />
    <Todos
      v-bind:todos="todos"
      v-on:del-todo="deleteTodo"
    />
  </div>
</template>

<script>
  import Todos from './components/Todos';
  import AddTodo from './components/AddTodo';
  import axios from 'axios';

  export default {
    name: 'app',
    components: {
      Todos,
      AddTodo
    },
    data() {
      return {
        todos: []
      }
    },
    methods: {
      deleteTodo(id) {
        axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
          .then(resp => this.todos = this.todos.filter(todo => todo.id !== id))
          .catch(error => console.log(error));
      },
      addTodo({ title, completed }) {
        axios.post('https://jsonplaceholder.typicode.com/todos', { title, completed })
          .then(resp => this.todos = [...this.todos, resp.data])
          .catch(error => console.log(error));
      }
    },
    created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(resp => this.todos = resp.data)
        .catch(error => console.log(error));
    }
  }
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
