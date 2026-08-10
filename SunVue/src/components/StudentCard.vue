<script setup lang="ts">
// Define the props passed from the parent component
defineProps<{
  name: string
  surname: string
  gpa: number
}>()
</script>

<template>
  <div class="border border-gray-300 rounded-lg p-4 my-2.5 w-full max-w-[300px] bg-gray-50 shadow-md">
    <h3>{{ name }} {{ surname }}</h3>
    <p><strong>GPA:</strong> {{ gpa }}</p>
  </div>
</template>