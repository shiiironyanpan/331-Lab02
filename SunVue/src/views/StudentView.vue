<script setup lang="ts">
import StudentCard from '@/components/StudentCard.vue'
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'

// Define a simple interface for the student data
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
      console.error('There was an error fetching students!', error)
    })
})
</script>

<template>
  <div class="student-view">
    <h1>Student List</h1>
    <div class="students">
      <!-- Loading state -->
      <div v-if="!students">Loading students...</div>
      
      <!-- Display students on cards -->
      <template v-else v-for="student in students" :key="student.name + student.surname">
        <StudentCard 
          :name="student.name" 
          :surname="student.surname" 
          :gpa="student.gpa" 
        />
      </template>
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
.students {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
</style>