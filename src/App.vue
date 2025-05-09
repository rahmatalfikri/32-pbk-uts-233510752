<script setup>
import { ref, computed } from 'vue'

const tasks = ref([])
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

const removeTask = (taskId) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId)
}

const countTasks = computed(() => tasks.value.length)

</script>

<template>
  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task">
    <button @click="addTask">Add Task</button>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" v-model="task.completed">
        {{ task.title }} - {{ task.completed ? 'Completed' : 'Not Completed' }}
        <button @click="removeTask(task.id)">Remove</button>
      </li>
    </ul>
    <p>Total Tasks: {{ countTasks }}</p>
  </div>
</template>

<style scoped></style>
