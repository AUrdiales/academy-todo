<template>
  <label class="todo--item">
    <input type="checkbox" @click="emit('completeTodo', props.todo.id)" :checked="todo.completed" />
    <span :class="['todo--title', { completed: props.todo.completed }]">{{ props.todo.title }}</span>
  </label>
  <BaseButton type="delete" @click="emit('removeTodo', props.todo.id)">🗑️</BaseButton>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue'
import BaseButton from './BaseButton.vue'
const props = defineProps({
  todo: {
    type: Object,
    required: true
  }
})
const emit = defineEmits(['completeTodo', 'removeTodo'])
</script>

<style scoped>
.todo--title {
  margin-left: 10px;
}

.todo--item {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.completed {
  color: #22c522;
}
</style>
