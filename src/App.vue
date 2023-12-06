<script setup>
  import { store } from './store.js'
  import CalculatorMain from './components/CalculatorMain.vue'
</script>

<template>
  <CalculatorMain />
  <div class="result">{{ store.result }}</div>
</template>