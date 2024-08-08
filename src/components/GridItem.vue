<template>
  <div class="bg-gray-600 p-4 rounded border border-white flex-1">
    <h1 class="font-bold text-xl mb-8">{{ title }}</h1>
    <ul class="flex flex-col gap-3" v-if="todos.length > 0">
      <Todo
        v-for="todo in todos"
        :key="todo.id"
        :text="todo.text"
        @next="$emit('previous', todo)"
        @previous="$emit('next', todo)"
      />
    </ul>
    <div v-else class="text-gray-400 flex flex-col items-center">
      <span class="text-3xl mb-6">╳</span>
      <p class="uppercase">No todos yet</p>
    </div>
    <form v-if="withAddForm" class="flex gap-3 mt-12" @submit.prevent="addTodo">
      <input
        type="text"
        class="w-full p-2 rounded text-gray-800 outline-none"
        v-model="todo"
      />
      <button class="bg-blue-500 text-white px-4 py-2 rounded">Add</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Todo from './Todo.vue'

defineProps({
  title: {
    type: String,
    default: 'Hello World'
  },
  todos: {
    type: Array,
    default: () => []
  },
  withAddForm: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['addTodo', 'next', 'previous'])

const todo = ref('')

const addTodo = () => {
  emit('addTodo', { text: todo.value, status: 'pending', completed: false })
  todo.value = ''
}
</script>
