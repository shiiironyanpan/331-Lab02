<script setup lang="ts">
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'

interface Student {
  name: string
  surname: string
  gpa: number
}

const students = ref<Student[] | null>(null)

onMounted(() => {
  StudentService.getStudents()
    .then((response) => {
      console.log(response.data)
      students.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <div class="student-view">
    <h1>Student List</h1>
    <div class="student-grid">
      <div v-if="!students">Loading students...</div>
      <div v-else v-for="(student, index) in students" :key="index" class="student-card">
        <h2>{{ student.name }} {{ student.surname }}</h2>
        <p>GPA: {{ student.gpa }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.student-view {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.student-grid {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  width: 100%;
  max-width: 400px;
}

.student-card {
  padding: 20px;
  width: 250px;
  cursor: pointer;
  border: 1px solid #39495c;
  border-radius: 8px;
  margin-bottom: 18px;
  text-align: left;
}

.student-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2);
}

.student-card h2 {
  font-size: 18px;
  margin: 0 0 8px 0;
}

.student-card p {
  font-size: 14px;
  margin: 0;
  color: #42b983;
}
</style>