<template>
  <div>
    <h2>Todos Page</h2>
    <router-link to="/">Home</router-link>
    <hr />
    <TodoAdd @add-todo="addTodo" />
    <div v-if="!loading">
      <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not completed</option>
      </select>
    </div>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="todosFiltered.length"
      :todos="todosFiltered"
      @remove-todo="removeTodo"
    />
    <h3 v-else class="todos-empty">No todos</h3>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import TodoAdd from '@/components/TodoAdd'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all',
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json
          this.loading = false
        }, 1000)
      })
  },
  computed: {
    todosFiltered() {
      switch (this.filter) {
        case 'completed':
          return this.todos.filter(item => item.completed)
        case 'not-completed':
          return this.todos.filter(item => !item.completed)
        default:
          return this.todos
      }
    },
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(item => item.id !== id)
    },

    addTodo(newTodo) {
      this.todos.push(newTodo)
    },
  },
  components: {
    TodoList,
    TodoAdd,
    Loader,
  },
}
</script>

<style scoped>
select {
  margin: 0 auto 1rem;
}

.todos-empty {
  border: 1px solid lightgrey;
  border-radius: 0.3rem;
  padding: 0.5rem 1rem;
  max-width: 600px;
  margin: 0 auto 1rem;
  box-sizing: border-box;
}
</style>
