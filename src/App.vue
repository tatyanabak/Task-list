<template>
  <div id="app">
    <h1>Список задач</h1>
    <hr>
    <AddTodo v-on:add-todo = "addTodo"/>
    <select v-model="filter">
      <option value="all">Все задачи</option>
      <option value="completed">Выполненные</option>
      <option value="not-completed">Невыполненные</option>
    </select>
    <TodoList
        v-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        v-on:remove-todo = "removeTodo"
    />
    <p v-else>Задач не найдено</p>
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo";
import TodoList from '@/components/TodoList.vue'

export default {
  name: 'App',

  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }
      else if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }
      else if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
      else {
        return this.todos
      }
    }
  },

  data() {
    return {
      todos: [
        {id: 1, title: 'task1', completed: false},
        {id: 2, title: 'task2', completed: false},
        {id: 3, title: 'task3', completed: false},
      ],
      filter: 'all',
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    AddTodo,
    TodoList
  }
}
</script>

<style scoped>
  select {
    margin-top: 10px;
  }
</style>
