<template>
  <main class="main-container">
    <form class="form-container" @submit.prevent="addTodo">
      <div class="input-container">
        <label>Add a to-do</label>
        <input class="input" v-model="todoTitle" />
      </div>
      <BaseButton type="submit">Add</BaseButton>
    </form>
    <span> {{ completedPercentage }}% of to-dos completed</span>
    <div class="todo-container" v-for="todo in todos" :key="todo.id">
      <TodoItem @complete-todo="completeTodo" @remove-todo="removeTodo" :todo="todo" />
    </div>
  </main>
</template>

<script setup>
import { computed, ref } from 'vue'
import BaseButton from '../components/BaseButton.vue'
import TodoItem from '../components/TodoItem.vue'

const todos = ref([])
const todoTitle = ref('')

const addTodo = () => {
  if (todoTitle.value.trim().length > 0) {
    const todo = {
      id: todos.value.length + 1,
      title: todoTitle.value,
      completed: false
    }
    todos.value.push(todo)
    todoTitle.value = ''
  }
}

const completeTodo = (id) => {
  const todo = todos.value.find((oldTodo) => id === oldTodo.id)
  todo.completed = !todo.completed
}

const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const completedPercentage = computed(() => {
  const completedTodos = todos.value.filter((todo) => todo.completed)
  const percentage = (completedTodos.length * 100) / todos.value.length || 0
  return percentage.toFixed(0)
})
</script>

<style scoped>
/* todo-app styles */
.main-container {
  margin: auto;
}
.form-container {
  display: flex;
  gap: 1rem;
}

.input-container {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  margin: 4px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-shadow: inset 0 1px 3px #ddd;
  border-radius: 4px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding-left: 20px;
  padding-right: 20px;
  padding-top: 12px;
  padding-bottom: 12px;
}
.todo-container {
  display: grid;
  grid-auto-flow: column;
  grid-template-columns: 75% 25%;
}
</style>
