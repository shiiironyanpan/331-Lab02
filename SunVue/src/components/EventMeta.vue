<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="event-meta">
    <span>{{ event.category }}</span>
    <span>{{ event.organizer }}</span>
  </div>
</template>

<style scoped>
.event-meta {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  font-size: 14px;
}
</style>