<template>
  <div>
    <li>
      <span v-bind:class="{done: todo.completed}">
        <input type="checkbox"
               v-on:change="todo.completed = !todo.completed">
        <strong>{{index + 1}}</strong>
        {{todo.title | lowerCase}}
      </span>
      <button v-on:click="$emit('remove-todo',todo.id)">
        &times;
      </button>
    </li>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    lowerCase(value) {
      return value.toLowerCase()
    }
  }
}
</script>

<style scoped>
  li {
    border-bottom: 1px solid grey;
    padding: 10px;
    display: flex;
    justify-content: space-between;
  }

  .done {
    text-decoration: line-through;
  }
</style>