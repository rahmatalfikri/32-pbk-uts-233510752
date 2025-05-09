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
  <div class="min-h-screen bg-yellow-50 flex items-start justify-center p-8">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full max-w-5xl">

      <!-- Left: Task List -->
      <div class="bg-white rounded-2xl shadow-lg p-6 space-y-4">
        <h2 class="text-2xl font-bold text-yellow-600 mb-2">📋 Daftar Tugas</h2>
        <ul class="space-y-3 max-h-96 overflow-y-auto pr-2">
          <li
            v-for="task in filteredTasks"
            :key="task.id"
            class="flex items-center justify-between bg-yellow-100 rounded-lg px-4 py-2 shadow-sm"
          >
            <div class="flex items-center gap-3">
              <input type="checkbox" v-model="task.completed" class="accent-yellow-500 w-5 h-5" />
              <span :class="task.completed ? 'line-through text-gray-400' : 'text-gray-800'">
                {{ task.title }}
              </span>
            </div>
            <button
              @click="removeTask(task.id)"
              class="text-red-500 hover:text-red-700 text-sm font-semibold"
            >
              Hapus
            </button>
          </li>
        </ul>
      </div>

      <!-- Right: Control Panel -->
      <div class="bg-white rounded-2xl shadow-lg p-6 space-y-6">
        <h2 class="text-2xl font-bold text-yellow-600 mb-4">⚙️ Panel Kontrol</h2>

        <div class="space-y-3">
          <input
            v-model="newTask"
            placeholder="Tulis tugas baru..."
            class="w-full px-4 py-2 rounded-lg border border-yellow-300 focus:outline-yellow-500"
            @keyup.enter="addTask"
          />
          <button
            @click="addTask"
            class="w-full bg-yellow-400 hover:bg-yellow-300 text-yellow-900 font-semibold py-2 rounded-lg transition"
          >
            Tambahkan Tugas
          </button>
        </div>

        <div class="space-y-2">
          <label class="text-yellow-700 font-medium">Filter Tugas</label>
          <select
            v-model="filter"
            class="w-full px-4 py-2 rounded-lg border border-yellow-300 text-yellow-800 focus:outline-yellow-500"
          >
            <option value="all">Semua</option>
            <option value="completed">Selesai</option>
            <option value="not-completed">Belum Selesai</option>
          </select>
        </div>

        <p class="text-center text-lg font-medium text-yellow-700 mt-4">
          Total Tugas: {{ countTasks }}
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
