<template>
  <form @submit.prevent="onSubmit">
    <input
      v-model="title"
      @keydown.enter="onSubmit"
      type="text"
      placeholder="What needs to be done"
    />
    <button type="submit">Add Todo</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
    }
  },

  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false,
        }

        this.$emit('add-todo', newTodo)
        this.title = ''
      }
    },
  },
}
</script>

<style scoped>
form {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto 0.8rem;
  max-width: 600px;
}

button {
  width: 15%;
}

input {
  width: calc(85% - 0.6rem);
  margin-right: 0.6rem;
}
</style>
