<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="flex justify-end gap-3 text-sm">
    <span>{{ event.category }}</span>
    <span>{{ event.organizer }}</span>
  </div>
</template>