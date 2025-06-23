<template>
  <div class="border rounded-lg shadow p-4 bg-white">
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