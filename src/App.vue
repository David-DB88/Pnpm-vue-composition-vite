<template>
  <div id="app">
    <Header/>
    <Filter @filter="filterTodo"/>
    <main class="app-main">
      <TodoList :todo="computedTodos"
                @implementTodo="implementTodo"
                @removeTodo="removeTodo"
      />
      <AddFormTodo @submit="addTask"/>
    </main>
    <Footer :stats="statsTodos"/>
  </div>
</template>

<script setup lang="ts">
import Header from "./components/Header.vue";
import Filter from "./components/Filter.vue";
import TodoList from "./components/TodoList.vue";
import Footer from "./components/Footer.vue";
import AddFormTodo from "./components/AddFormTodo.vue";
import {computed, ref} from "vue";
import {TodoTypes} from "./Types/todoTypes";

//state
const todo = ref<TodoTypes[]>([
  {id: 1, todo: 'Learn the basics of Vue', completed: true},
  {id: 2, todo: 'Learn the basics of Typescript', completed: false},
  {id: 3, todo: 'Subscribe to the channel', completed: false}
])
const filteredTodos = ref<string>('')

//methods
const implementTodo =(id)=>{
 todo.value = todo.value.map(e=> (e.id === id )? {...e, completed: !e.completed}: e)
}
const removeTodo =(id)=>{
 todo.value = todo.value.filter(e=> e.id !== id )
}
const addTask =(event)=>{
  todo.value.push(event)
}
const filterTodo = (filter: string)=>{
  filteredTodos.value = filter
}
//Computed
const activeTodos = computed(()=>{
  return todo.value.filter(e =>e.completed === false)
})
const doneTodos = computed(()=>{
  return todo.value.filter(e=>e.completed === true)
})
const computedTodos = computed(()=>{
  switch (filteredTodos.value){
    case  "Active":
      return  activeTodos
    case 'Done':
      return  doneTodos
    default:
      return todo.value
  }
})
const statsTodos = computed(()=>{
  return {
    active: activeTodos.value.length,
    done: doneTodos.value.length
  }
})

</script>

<style scoped>
</style>
