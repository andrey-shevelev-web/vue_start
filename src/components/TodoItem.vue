<template>
  <li>
    <span :class="{ done: todo.completed }">
      <input @change="todo.completed = !todo.completed" type="checkbox" />
      <strong>{{ index + 1 }}</strong>
      {{ todo.title | capitalize }}
    </span>
    <button class="rm-button" @click="$emit('remove-todo', todo.id)">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  filters: {
    capitalize(value) {
      return value[0].toUpperCase() + value.slice(1).toLowerCase()
    },
  },
}
</script>

<style scoped>
li {
  border: 1px solid lightgrey;
  border-radius: 0.3rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 1rem;
  margin-bottom: 1rem;
}

input {
  margin-right: 1rem;
}

.rm-button {
  background: red;
  color: #fff;
  border-radius: 20%;
  font-weight: bold;
}

.done {
  text-decoration: line-through;
}
</style>
