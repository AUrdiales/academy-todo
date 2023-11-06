<template>
  <main class="main-container">
    <form class="form-container">
      <div class="input-container">
        <label>Add a todo</label>
        <input class="input" />
      </div>
      <button class="submit-button">Add todo</button>
    </form>
    <span>% of to-dos completed</span>
    <div class="todo-container">
      <label class="todo-item">
        <input type="checkbox" /><span class="todo-title">Task 1</span>
      </label>
      <button class="button-remove">🗑️</button>
    </div>
    <div class="todo-container">
      <label class="todo-item">
        <input type="checkbox" /><span class="todo-title"
          >Task 2 that has a lot of characters</span
        >
      </label>
      <button class="button-remove">🗑️</button>
    </div>
    <div class="todo-container">
      <label class="todo-item">
        <input type="checkbox" /><span class="todo-title">Task 3</span>
      </label>
      <button class="button-remove">🗑️</button>
    </div>
  </main>
</template>

<script setup></script>

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

.submit-button {
  align-self: end;
  background-color: #25c26c;
  border: none;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
}

.submit-button:hover {
  background-color: #157c23;
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
  color: #dd1b1b;
  white-space: nowrap;
}

.completed {
  color: #22c522;
}

.button-remove {
  justify-self: center;
}
</style>
