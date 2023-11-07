<template>
  <label class="todo--item">
    <input type="checkbox" :checked="props.todo.completed" />
    <span :class="['todo--title', { completed: props.todo.completed }]">{{
      props.todo.title
    }}</span>
  </label>
</template>

<script setup>
const props = defineProps({
  todo: {
    type: Object,
    required: true
  }
})
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
