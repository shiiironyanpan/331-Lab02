<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventMeta from '@/components/EventMeta.vue'
import type { Event } from '@/types'
import { ref, computed, watchEffect } from 'vue'
import EventService from '@/services/EventService'
import { useRouter } from 'vue-router'

const props = defineProps({
    page: {
        type: Number,
        required: true
    },
    perPage: {
        type: Number,
        default: 2
    }
})

const events = ref<Event[] | null>(null)
const totalEvents = ref<number>(0)
const page = computed(() => props.page)
const hasNextPage = computed(() => {
    const totalPages = Math.ceil(totalEvents.value / props.perPage)
    return page.value < totalPages
})
const router = useRouter()

watchEffect(() => {
    events.value = null
    EventService.getEvents(props.perPage, page.value)
        .then((response) => {
            events.value = response.data
            totalEvents.value = response.headers['x-total-count']
        })
        .catch(() => {
            router.push({ name: 'network-error-view' })
        })
})
</script>

<template>
  <div class="home">
    <h1>Events For Good</h1>
    <div class="events">
      <div v-if="!events">Loading events...</div>
      <template v-else v-for="event in events" :key="event.id">
        <EventCard :event="event" />
        <EventMeta :event="event" />
      </template>
    </div>
    <div class="pagination">
      <RouterLink
          id="page-prev"
          :to="{ name: 'event-list-view', query: { page: page - 1, perPage: perPage } }"
          rel="prev"
          v-if="page != 1"
          >&#60; Prev Page</RouterLink>
      <RouterLink
          id="page-next"
          :to="{ name: 'event-list-view', query: { page: page + 1, perPage: perPage } }"
          rel="next"
          v-if="hasNextPage"
          >Next Page &#62;</RouterLink>
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}
.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}
#page-prev {
  text-align: left;
}
#page-next {
  text-align: right;
}
</style>