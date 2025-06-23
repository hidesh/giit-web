<template>
  <div class="p-6 max-w-5xl mx-auto">
    <h1 class="text-3xl font-bold mb-6 text-center">Alle Events</h1>
    <div v-if="!data"><p>Loading...</p></div>
    <div v-else-if="events.length === 0"><p>Ingen events fundet.</p></div>
    <div v-else class="grid md:grid-cols-2 gap-6">
      <div
        v-for="event in events"
        :key="event.id"
        class="border rounded p-4 shadow"
      >
        <NuxtLink :to="`/event/${event.id}`">
          <img
            :src="fullImageUrl(event.image)"
            alt="Event image"
            class="rounded mb-2 w-full h-48 object-cover"
          />
          <h2 class="text-xl font-bold">{{ event.title }}</h2>
          <p class="text-gray-600 text-sm">{{ event.date }} – {{ event.location }}</p>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
const { data } = await useFetch('http://localhost:8055/items/events', {
  params: {
    fields: 'id,title,image,date,location,description,status',
    deep: {
      host: {
        _filter: {},
        _fields: 'id,name,image'
      }
    },
    filter: {
      status: {
        _eq: 'published'
      }
    },
    sort: '-date'
  }
})

const events = computed(() => data.value?.data ?? []) // fallback hvis data er null

  console.log('Fetched events:', events)

const fullImageUrl = (path) =>
  `http://localhost:8055/assets/${path}`
</script>