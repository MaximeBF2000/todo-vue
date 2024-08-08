<template>
  <li class="w-full bg-white text-gray-800 px-6 py-3 rounded">
    <label class="w-full h-full flex gap-3 justify-between items-center">
      <span>{{ text }}</span>
      <div class="flex gap-3 items-center">
        <span
          class="cursor-pointer"
          v-if="status !== 'pending'"
          @click="$emit('previous')"
          >←</span
        >
        <span
          class="cursor-pointer"
          v-if="status !== 'done'"
          @click="$emit('next')"
          >→</span
        >
      </div>
    </label>
  </li>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps({
  id: {
    type: String,
    default: crypto.randomUUID()
  },
  text: {
    type: String,
    required: true
  },
  completed: {
    type: Boolean,
    default: false
  },
  status: {
    type: String,
    default: 'pending'
  }
})

defineEmits(['next', 'previous'])
</script>
