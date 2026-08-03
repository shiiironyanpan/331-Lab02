<script setup lang="ts">
// Define the props passed from the parent component
defineProps<{
  name: string
  surname: string
  gpa: number
}>()
</script>

<template>
  <div class="student-card">
    <h3>{{ name }} {{ surname }}</h3>
    <p><strong>GPA:</strong> {{ gpa }}</p>
  </div>
</template>

<style scoped>
.student-card {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 16px;
  margin: 10px 0;
  width: 100%;
  max-width: 300px;
  background-color: #f9f9f9;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>