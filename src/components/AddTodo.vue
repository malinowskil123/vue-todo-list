<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        name="title"
        v-model="title"
        placeholder="Add Todo..."
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
  export default {
    name: 'AddTodo',

    data() {
      return {
        title: this.title,
      }
    },

    methods: {
      addTodo(e) {
        if (this.title) {
          e.preventDefault()
          const newTodo = {
            title: this.title,
            completed: false,
          }
          // send up to parent by emmmiting a event
          this.$emit('add-todo', newTodo)
          this.title = ''
        } else alert('Please enter a todo into the input field!')
      },
    },
  }
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type='text'] {
    flex: 10;
    padding: 5px;
  }
  input[type='submit'] {
    flex: 2;
  }
</style>
