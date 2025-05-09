<script setup>
import { ref, computed } from 'vue'

const tasks = ref([])
const newTask = ref('')
const filter = ref('all')

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

const filteredTasks = computed(() => {
  if (filter.value === 'completed') {
    return tasks.value.filter(task => task.completed)
  } else if (filter.value === 'not-completed') {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})

</script>

<template>
  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task">
    <button @click="addTask">Add Task</button>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <ul>
      <li v-for="task in filteredTasks" :key="task.id">
        <input type="checkbox" v-model="task.completed">
        {{ task.title }} - {{ task.completed ? 'Completed' : 'Not Completed' }}
        <button @click="removeTask(task.id)">Remove</button>
      </li>
    </ul>
    <p>Total Tasks: {{ countTasks }}</p>
  </div>
</template>

<style scoped></style>
