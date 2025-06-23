<template>
  <div class="p-8 space-y-6">
    <h1 class="text-3xl font-bold">Kommende Events</h1>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <EventCard
        v-for="event in events"
        :key="event.id"
        :title="event.title"
        :date="event.date"
        :description="event.description"
      />
    </div>
  </div>
</template>

<script setup>
import EventCard from '~/components/EventCard.vue'

const events = [
  {
    id: 1,
    title: 'Tech Talks 2025',
    date: '15. juli 2025',
    description: 'Et oplæg om kvinder i tech og netværksmuligheder.'
  },
  {
    id: 2,
    title: 'AI Bootcamp',
    date: '22. august 2025',
    description: 'En hel dag med workshops om AI og ML.'
  },
  {
    id: 3,
    title: 'Coding for Change',
    date: '5. september 2025',
    description: 'Et community-event med fokus på impact-projekter.'
  }
]
</script>