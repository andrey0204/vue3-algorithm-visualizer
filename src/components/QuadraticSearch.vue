<template>
  <div class="p-4 max-w-xl mx-auto">
    <h2 class="text-xl font-bold mb-2">🧪 Comparación Cuadrática (O(n²))</h2>

    <button @click="startCheck" class="bg-blue-500 text-white px-4 py-1 rounded">Buscar duplicados</button>

    <div class="grid grid-cols-10 gap-2 mt-4">
      <div
        v-for="(num, index) in arr"
        :key="index"
        class="border px-2 py-1 text-center transition-all duration-300 ease-in-out"
        :class="{
          'bg-yellow-300': index === i,
          'bg-red-300': index === j,
          'bg-green-400 scale-110 font-bold': duplicateIndex === index
        }"
      >
        {{ num }}
      </div>
    </div>

    <div class="mt-4 text-sm space-y-1">
      <p>🔁 Paso actual: {{ step }}</p>
      <p>🔄 Comparando: i = {{ i }}, j = {{ j }}</p>
      <p>⏱ Tiempo total: <span class="font-semibold text-blue-600">{{ elapsedTime }} ms</span></p>
    </div>

    <div v-if="duplicateIndex !== null" class="text-green-600 font-bold mt-2">
      ✅ Duplicado encontrado en el índice {{ duplicateIndex }}
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const arr = ref([1, 3, 5, 7, 3, 9, 11, 13, 15, 17]) // contiene un duplicado en la posición 1 y 4

const i = ref<number | null>(null)
const j = ref<number | null>(null)
const step = ref(0)
const duplicateIndex = ref<number | null>(null)
const elapsedTime = ref<string>('0')

const sleep = (ms: number) => new Promise(resolve => setTimeout(resolve, ms))

async function startCheck() {
  step.value = 0
  duplicateIndex.value = null
  const start = performance.now()

  for (let outer = 0; outer < arr.value.length - 1; outer++) {
    i.value = outer
    for (let inner = outer + 1; inner < arr.value.length; inner++) {
      j.value = inner
      step.value++
      await sleep(150)

      if (arr.value[outer] === arr.value[inner]) {
        duplicateIndex.value = inner
        const end = performance.now()
        elapsedTime.value = (end - start).toFixed(2)
        return
      }
    }
  }

  const end = performance.now()
  elapsedTime.value = (end - start).toFixed(2)
}
</script>
