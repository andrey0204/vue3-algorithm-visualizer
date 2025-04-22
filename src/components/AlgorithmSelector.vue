<template>
  <div class="p-4 max-w-6xl mx-auto">
    <h1 class="text-2xl font-bold text-center mb-6">🧠 Visualizador de Complejidad Algorítmica</h1>

    <div class="flex justify-center mb-4">
      <el-tabs v-model="activeTab" type="card">
        <el-tab-pane label="O(1) - Constante" name="constant">
          <ConstantAccess />
        </el-tab-pane>
        <el-tab-pane label="O(n) - Lineal" name="linear">
          <LinearSearch />
        </el-tab-pane>
        <el-tab-pane label="O(n²) - Cuadrática" name="quadratic">
          <QuadraticSearch />
        </el-tab-pane>
        <el-tab-pane label="O(log n) - Logarítmica" name="logarithmic">
          <BinarySearchVisualizer />
        </el-tab-pane>
      </el-tabs>
    </div>

  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

// Importa tus componentes visualizadores
import ConstantAccess from './ConstantAccess.vue'
import LinearSearch from './LinearSearch.vue'
import QuadraticSearch from './QuadraticSearch.vue'
import BinarySearchVisualizer from './BinarySearchVisualizer.vue'

const activeTab = ref('constant')
</script>
