<template>
  <div class="p-4 max-w-xl mx-auto">
    <h2 class="text-xl font-bold mb-2">⚡ Acceso Constante (O(1))</h2>

    <div class="flex items-center gap-2 mb-4">
      <label for="index">Índice:</label>
      <input
        v-model.number="index"
        id="index"
        type="number"
        min="0"
        :max="arr.length - 1"
        class="border px-2 py-1 rounded w-20"
      />
      <button @click="access" class="bg-blue-500 text-white px-4 py-1 rounded">Acceder</button>
    </div>

    <div class="grid grid-cols-10 gap-2 mt-2">
      <div
        v-for="(num, i) in arr"
        :key="i"
        class="border px-2 py-1 text-center transition-all duration-300 ease-in-out"
        :class="{
          'bg-green-400 scale-110 font-bold': i === index
        }"
      >
        {{ num }}
      </div>
    </div>

    <div class="mt-4 text-sm space-y-1">
      <p>🔁 Paso actual: {{ step }}</p>
      <p>📍 Índice accedido: {{ index }}</p>
      <p>⏱ Tiempo total: <span class="font-semibold text-blue-600">{{ elapsedTime }} ms</span></p>
    </div>

    <div v-if="result !== null" class="mt-2 font-bold text-green-600">
      ✅ Valor accedido: {{ result }}
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const arr = ref([...Array(20)].map((_, i) => i + 1)) // [1, 2, ..., 20]
const index = ref<number>(0)
const result = ref<number | null>(null)
const step = ref<number>(0)
const elapsedTime = ref<string>('0')

function access() {
  const start = performance.now()
  step.value = 1
  result.value = arr.value[index.value]
  const end = performance.now()
  elapsedTime.value = (end - start).toFixed(2)
}
</script>
