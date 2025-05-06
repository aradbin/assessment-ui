<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'

const employees = ref([])

const fetchEmployees = async () => {
  try {
    const response = await axios.get('http://localhost:8000/api/employees')
    employees.value = response.data
  } catch (error) {
    alert('Failed to fetch employees.')
  }
}

onMounted(fetchEmployees)
</script>

<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">Employee List</h1>
    <table class="table-auto w-full border-collapse border border-gray-300">
      <thead>
        <tr>
          <th class="border border-gray-300 px-4 py-2">ID</th>
          <th class="border border-gray-300 px-4 py-2">Name</th>
          <th class="border border-gray-300 px-4 py-2">Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td class="border border-gray-300 px-4 py-2">{{ employee.id }}</td>
          <td class="border border-gray-300 px-4 py-2">{{ employee.name }}</td>
          <td class="border border-gray-300 px-4 py-2">{{ employee.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>