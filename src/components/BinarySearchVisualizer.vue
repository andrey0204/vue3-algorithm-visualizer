<template>
  <div class="p-4 max-w-xl mx-auto">
    <h2 class="text-xl font-bold mb-2">🔍 Búsqueda Binaria Visual (O(log n))</h2>

    <input v-model.number="target" type="number" class="border px-2 py-1 mr-2 rounded" placeholder="Número a buscar" />
    <button @click="startSearch" class="bg-blue-500 text-white px-4 py-1 rounded">Buscar</button>

    <div class="grid grid-cols-10 gap-2 mt-4">
      <div
        v-for="(num, index) in arr"
        :key="index"
        class="border px-2 py-1 text-center transition-all duration-300 ease-in-out"
        :class="{
          'bg-yellow-300': index === mid,
          'bg-green-400 scale-110 font-bold': index === result,
          'opacity-30': index < low || index > high
        }"
      >
        {{ num }}
      </div>
    </div>

    <div class="mt-4 text-sm space-y-1">
      <p>🔁 Paso actual: {{ step }}</p>
      <p>📍 Índices → low: {{ low }}, mid: {{ mid }}, high: {{ high }}</p>
      <p>⏱ Tiempo total: <span class="font-semibold text-blue-600">{{ elapsedTime }} ms</span></p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const arr = ref([...Array(20)].map((_, i) => i + 1)) // [1, 2, ..., 20]
const target = ref<number | null>(null)

const low = ref(0)
const high = ref(arr.value.length - 1)
const mid = ref<number | null>(null)
const step = ref(0)
const result = ref<number | null>(null)
const elapsedTime = ref<string>('0')

const sleep = (ms: number) => new Promise(resolve => setTimeout(resolve, ms))

async function startSearch() {
  result.value = null
  low.value = 0
  high.value = arr.value.length - 1
  step.value = 0

  const start = performance.now()

  while (low.value <= high.value) {
    step.value++
    mid.value = Math.floor((low.value + high.value) / 2)
    await sleep(300)

    if (arr.value[mid.value] === target.value) {
      result.value = mid.value
      break
    } else if (arr.value[mid.value] < target.value!) {
      low.value = mid.value + 1
    } else {
      high.value = mid.value - 1
    }
  }

  const end = performance.now()
  elapsedTime.value = (end - start).toFixed(2)
}
</script>
