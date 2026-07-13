<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventMeta from '@/components/EventMeta.vue'
import type { Event } from '@/types'
import { ref, onMounted } from 'vue'       // added onMounted
import axios from 'axios'                  // added

const events = ref<Event[] | null>(null)   // changed from array to null

onMounted(() => {
  axios
    .get('https://my-json-server.typicode.com/shiiironyanpan/672115048/events')
    .then((response) => {
      console.log(response.data)           // show data in console
      events.value = response.data         // assign to events
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <div class="home">
    <h1>Events For Good</h1>
    <div class="events">
      <!-- Show loading or empty state if events is null -->
      <div v-if="!events">Loading events...</div>
      <template v-else v-for="event in events" :key="event.id">
        <EventCard :event="event" />
        <EventMeta :event="event" />
      </template>
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>