<template>
  <main class="main-container">
    <form class="form-container" @submit.prevent="addTodo">
      <div class="input-container">
        <label>Add a to-do</label>
        <input class="input" v-model="todoTitle" />
      </div>
      <button class="button--submit">Add</button>
    </form>
    <span> {{ completedPercentage }}% of to-dos completed</span>
    <div class="todo-container" v-for="todo in todos" :key="todo.id">
      <label class="todo-item">
        <input type="checkbox" @click="completeTodo(todo.id)" :checked="todo.completed" /><span
          :class="['todo-title', { completed: todo.completed }]"
          >{{ todo.title }}</span
        >
      </label>
      <button class="button--remove" @click="removeTodo(todo.id)">🗑️</button>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      todoTitle: ''
    }
  },
  methods: {
    addTodo() {
      if (this.todoTitle.trim().length > 0) {
        const todo = {
          id: this.todos.length + 1,
          title: this.todoTitle,
          completed: false
        }
        this.todos.push(todo)
        this.todoTitle = ''
      }
    },
    completeTodo(id) {
      const todo = this.todos.find((oldTodo) => id === oldTodo.id)
      todo.completed = !todo.completed
    },
    removeTodo(id) {
      console.log(id)
      this.todos = this.todos.filter((todo) => todo.id !== id)
    }
  },
  computed: {
    completedPercentage() {
      const completedTodos = this.todos.filter((todo) => todo.completed)
      const percentage = (completedTodos.length * 100) / this.todos.length || 0
      return percentage.toFixed(0)
    }
  }
}
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
