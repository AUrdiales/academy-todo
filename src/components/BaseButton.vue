<template>
  <button :class="`button--${type}`">
    <slot></slot>
  </button>
</template>

<script setup>
import { defineProps } from 'vue'
const { type } = defineProps({
  type: {
    type: String,
    required: true
  }
})
</script>

<style scoped>
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

.button--remove {
  justify-self: center;
}
</style>
