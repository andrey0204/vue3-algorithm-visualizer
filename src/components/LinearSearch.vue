<template>
  <div class="p-4 max-w-xl mx-auto">
    <h2 class="text-xl font-bold mb-2">📏 Búsqueda Lineal (O(n))</h2>

    <input
      v-model.number="target"
      type="number"
      class="border px-2 py-1 mr-2 rounded"
      placeholder="Número a buscar"
    />
    <button @click="startSearch" class="bg-blue-500 text-white px-4 py-1 rounded">Buscar</button>

    <div class="grid grid-cols-10 gap-2 mt-4">
      <div
        v-for="(num, index) in arr"
        :key="index"
        class="border px-2 py-1 text-center transition-all duration-300 ease-in-out"
        :class="{
          'bg-yellow-300': index === current,
          'bg-green-400 scale-110 font-bold': index === result
        }"
      >
        {{ num }}
      </div>
    </div>

    <div class="mt-4 text-sm space-y-1">
      <p>🔁 Paso actual: {{ step }}</p>
      <p>📍 Índice actual: {{ current }}</p>
      <p>⏱ Tiempo total: <span class="font-semibold text-blue-600">{{ elapsedTime }} ms</span></p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const arr = ref([...Array(20)].map((_, i) => i + 1)) // [1, 2, ..., 20]
const target = ref<number | null>(null)

const current = ref<number | null>(null)
const result = ref<number | null>(null)
const step = ref(0)
const elapsedTime = ref<string>('0')

const sleep = (ms: number) => new Promise(resolve => setTimeout(resolve, ms))

async function startSearch() {
  result.value = null
  current.value = null
  step.value = 0
  const start = performance.now()

  for (let i = 0; i < arr.value.length; i++) {
    current.value = i
    step.value++
    await sleep(250)

    if (arr.value[i] === target.value) {
      result.value = i
      break
    }
  }

  const end = performance.now()
  elapsedTime.value = (end - start).toFixed(2)
}
</script>
