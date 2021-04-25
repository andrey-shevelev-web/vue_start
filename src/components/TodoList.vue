<template>
  <div>
    <ul>
      <TodoItem
        v-for="(todo, index) of todos"
        :key="todo.id"
        :todo="todo"
        :index="index"
        @remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'

export default {
  props: ['todos'],
  components: {
    TodoItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id)
    },
  },
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  max-width: 600px;
  margin: 0 auto;
}
</style>
