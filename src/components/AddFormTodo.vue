<template>
  <section class="add-todo">

    <form class="add-todo__form"  v-if="isVisibleForm" @submit.prevent="submitForm">
      <button class="close-button" type="button" @click="closeForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="task" class="input"/>
      </div>
      <button class="button button--filled" type="submit">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showFrom">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script setup lang="ts">
import {defineEmits, ref} from "vue";
import {TodoTypes} from "../Types/todoTypes";

const isVisibleForm = ref(false)
const task = ref('')



const showFrom =()=>{
  isVisibleForm.value = true
}
const closeForm =()=>{
  isVisibleForm.value = false
}

function submitForm() {
  emit('submit', {
    id: new Date(),
    todo: task.value,
    completed: false
  })
  task.value = ''
}

const emit = defineEmits({
  // Validate submit event
  submit: (task ) => {
    if (task) {
      return true
    } else {
      console.warn('Invalid submit event payload!')
      return false
    }
  }
})


// const emit = defineEmits<{
//   (e: 'addTask', obj: TodoTypes): void
// }>()

</script>

<style scoped>

</style>