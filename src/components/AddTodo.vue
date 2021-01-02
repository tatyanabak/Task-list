<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="newTodoItem">
    <button type="submit">Добавить задачу</button>
  </form>
</template>

<script>
export default {
  name: "AddTodo",

  data() {
    return {
      newTodoItem: ''
    }
  },

  methods: {
    onSubmit() {
      console.log('sdsd', this.newTodoItem);
      if (this.newTodoItem.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.newTodoItem,
          completed: false
        }

        this.$emit('add-todo', newTodo)
        this.newTodoItem = ''
      }
    }
  }
}
</script>

<style scoped>

</style>