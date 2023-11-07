<template>
  <main class="main-container">
    <form class="form-container" @submit.prevent="addTodo">
      <div class="input-container">
        <label>Add a to-do</label>
        <input class="input" v-model="todoTitle" />
      </div>
      <button class="button--submit">Add</button>
    </form>
    <span v-show="numberOfTodos"> {{ completedPercentage }}% of to-dos completed</span>
    <div class="todo-container" v-for="todo in todos" :key="todo.id">
      <label class="todo-item">
        <input type="checkbox" @change="completeTodo(todo.id)" :checked="todo.completed" /><span
          :class="['todo-title', { completed: todo.completed }]"
          >{{ todo.title }}</span
        >
      </label>
      <button class="button--remove" @click="removeTodo(todo.id)">🗑️</button>
    </div>
  </main>
</template>

<script setup>
import { computed, ref } from 'vue'

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

const numberOfTodos = computed(() => todos.value.length)

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

.button--submit {
  align-self: end;
  background-color: #25c26c;
  border: none;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
}

.button--submit:hover {
  background-color: rgba(37, 193, 107, 0.7);
}

/* todo list styles */
.todo-container {
  display: grid;
  grid-auto-flow: column;
  grid-template-columns: 75% 25%;
}
.todo-title {
  margin-left: 10px;
}

.todo-item {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.completed {
  color: #22c522;
}

.button--remove {
  justify-self: center;
}
</style>
