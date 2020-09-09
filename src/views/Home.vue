<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos
      v-bind:todos="todos"
      v-on:del-todo="deleteTodo"
      v-on:mark-complete="markComplete"
    />
  </div>
</template>

<script>
  import Todos from '../components/Todos.vue'
  import AddTodo from '../components/AddTodo.vue'
  import axios from 'axios'

  export default {
    name: 'Home',
    components: {
      Todos,
      AddTodo,
    },
    data() {
      return {
        todos: [],
      }
    },
    async created() {
      try {
        const response = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_limit=5'
        )
        this.todos = response.data
      } catch (err) {
        console.log(err.message)
      }
    },

    methods: {
      async markComplete(todo) {
        const { id, title, completed } = todo
        try {
          const response = await axios.put(
            `https://jsonplaceholder.typicode.com/todos/${id}`,
            {
              id,
              title,
              completed: !completed,
            }
          )
          const updatedTodo = response.data
          this.todos = this.todos.map((todo) =>
            todo.id === updatedTodo.id ? updatedTodo : todo
          )
          console.log(response.data)
        } catch (err) {
          console.log(err.message)
        }
      },

      async deleteTodo(id) {
        try {
          await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
          this.todos = this.todos.filter((todo) => todo.id !== id)
        } catch (err) {
          console.log(err.message)
        }
      },

      async addTodo(newTodo) {
        const { title, completed } = newTodo
        try {
          const response = await axios.post(
            'https://jsonplaceholder.typicode.com/todos',
            {
              title,
              completed,
            }
          )
          this.todos = [...this.todos, ...response.data]
        } catch (err) {
          console.log(err.message)
        }
        this.todos = [...this.todos, newTodo]
      },
    },
  }
</script>

<style>
  body {
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
