<template>
  <div class="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
    <EventCard
      v-for="event in events"
      :key="event.id"
      :title="event.title"
      :date="event.date"
      :description="event.description"
      @click="goToEvent(event.id)"
    />
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import EventCard from '~/components/EventCard.vue'

const router = useRouter()

const { data: events } = await useFetch('http://localhost:8055/items/events', {
  params: {
    fields: 'id,title,date,description',
  },
})

function goToEvent(id) {
  router.push(`/events/${id}`)
}
</script>