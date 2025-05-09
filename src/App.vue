<script setup>
import  { ref } from 'vue'

const tasks = ref([
  {
    id: 1,
    title: 'Task 1',
    completed: false
  },
  {
    id: 2,
    title: 'Task 2',
    completed: true
  },
  {
    id: 3,
    title: 'Task 3',
    completed: false
  }
])
const newTask = ref('')

const addTask = () => {
  if (newTask.value.trim() === '') return
  tasks.value.push({
    id: tasks.value.length + 1,
    title: newTask.value,
    completed: false
  })
  newTask.value = ''
}

</script>

<template>
  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task">
    <button @click="addTask">Add Task</button>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{ task.title }} - {{ task.completed ? 'Completed' : 'Not Completed' }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
