<template>
  <ul class="todo-list">
    <li v-for="item in props.todo"
        :key="item.id" class="todo-item "
        :class="{'todo-item--done': item.completed}"
        @click="emit('implementTodo', item.id)"
    >
      <div class="todo-item__status">
        <i class="bi bi-check2"></i>
      </div>
      <span class="todo-item__text">{{ item.todo }}</span>
      <button class="todo-item__remove-button" @click.stop="emit('removeTodo', item.id)">
        <i class="bi bi-trash3"></i>
      </button>
    </li>
  </ul>
</template>

<script setup lang="ts">
import {defineEmits, defineProps,} from "vue";
import {TodoTypes} from "../Types/todoTypes";

interface Props {
  todo: TodoTypes[]
}

const props = defineProps<Props>()


const emit = defineEmits<{
  (e: 'implementTodo', id: number): void
  (e: 'removeTodo', id: number): void
}>()
</script>

<style scoped>

</style>