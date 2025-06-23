<template>
  <div
    class="cursor-pointer border rounded-lg shadow p-4 bg-white hover:shadow-md transition"
    @click="$emit('click')"
  >
    <h2 class="text-xl font-semibold text-blue-700">{{ title }}</h2>
    <p class="text-gray-600">{{ date }}</p>
    <p class="mt-2 text-gray-800">{{ description }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  date: String,
  description: String
})
</script>