
<template>
  <div class="w-full h-full bg-gray-900 min-h-screen p-8 text-white flex flex-col justify-center">
    <h1 class="mb-4 text-center font-black uppercase text-6xl">Todo <span class="text-green-600">Vue</span></h1>
    <p class="text-center mb-20 text-gray-200">Made in 2 hours with React skills and ChatGPT prompt mastery ;)</p>
    <div class="flex gap-10 w-full">
      <GridItem title="Pending TODOS" :todos="pendingTodos" withAddForm @addTodo="todo => todos.push(todo)" @next="setStatusToCurrent" />
      <GridItem title="Working on it" :todos="currentTodos" @previous="setStatusToPending" @next="setStatusToDone" />
      <GridItem title="Dones" :todos="doneTodos" @previous="setStatusToCurrent" />
    </div>
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'
import GridItem from './components/GridItem.vue'
import Todo from './components/Todo.vue'

const todos = ref(JSON.parse(localStorage.getItem('todos') || '[]'))

watch(todos.value, (todos) => {
  localStorage.setItem('todos', JSON.stringify(todos))
})

const pendingTodos = computed(() => todos.value.filter(todo => todo.status === 'pending'))
const currentTodos = computed(() => todos.value.filter(todo => todo.status === 'current'))
const doneTodos = computed(() => todos.value.filter(todo => todo.status === 'done'))

const setStatusToCurrent = todo => {
  todo.status = 'current'
}

const setStatusToDone = todo => {
  todo.status = 'done'
}

const setStatusToPending = todo => {
  todo.status = 'pending'
}

</script>
