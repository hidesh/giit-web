<template>
  <!-- Event image background -->
  <div class="w-full">
    <img
      :src="fullImageUrl(event.image)"
      alt="Event banner"
      class="w-full h-[25vh] object-contain"
    />
  </div>

  <!-- Full eventcard -->
  <div class="flex flex-row items-center min-h-screen px-20">
    <div>
      
      <div class="text-left">
        <h1 class="text-3xl font-bold">Event Details</h1>
      </div>

      <div class="space-y-2">
        <div class="h-1 w-full bg-purple-300"></div>   <!-- lilla -->
        <div class="h-1 w-3/4 bg-sky-300"></div>       <!-- lyseblå -->
        <div class="h-1 w-2/4 bg-yellow-200"></div>    <!-- gul -->
      </div>

    </div>
    <div class="p-6 max-w-3xl mx-auto bg-white rounded shadow">
      <div v-if="isLoading">Loading...</div>
      <div v-else-if="!event">Event not found.</div>
      <div v-else>
        <img :src="fullImageUrl(event.image)" alt="Event image" class="w-full rounded mb-4" />
        <h1 class="text-2xl font-bold mb-2">{{ event.title }}</h1>
        <ClientOnly>
          <div class="text-gray-700 mb-4">
            <span v-if="event.location" class="block">Location: {{ event.location }}</span>
            <span v-if="event.date" class="block">Date: {{ new Date(event.date).toLocaleDateString() }}</span>
            <span v-if="event.date" class="block">Time: {{ new Date(event.date).toLocaleTimeString('da-DK', { hour: '2-digit', minute: '2-digit' }) }}</span>
          </div>

          <h2 class="text-xl font-bold mb-2">Description</h2>
          <p class="mb-4" v-html="event.description"></p>


        <div class="mt-6 flex items-center gap-4" v-if="event.host">
          <img :src="fullImageUrl(event.host.host_image)" alt="Host image" class="w-12 h-12 rounded-full" />
          <span class="text-gray-800 font-medium">{{ event.host.host_name }}</span>
          <p class="text-gray-600 text-sm" v-html="event.host.host_bio"></p>
        </div>
        </ClientOnly>
      </div>
      
    </div>
  </div>

</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const isLoading = ref(true)
const event = ref(null)

const fullImageUrl = (path) => `http://localhost:8055/assets/${path}`

const fetchEvent = async () => {
  try {
    const res = await $fetch(`http://localhost:8055/items/events/${route.params.id}`, {
      params: {
        fields: 'title,date,description,image,location,host.host_name,host.host_image,host.host_bio'
      }
    })
    event.value = res.data
  } catch (e) {
    console.error('Failed to fetch event:', e)
  } finally {
    isLoading.value = false
  }
}

await fetchEvent()
</script>