<script setup>
  import { ref } from 'vue';
  import { store } from '../store.js'
  const currentValue = ref('')
  const currentOperations = ref('')
  const input = ref(null)
  const setCalcDate = (operator) => {
      store.calculator.num1 = +currentValue.value
      currentValue.value = ''
      currentOperations.value = operator
      input.value.focus()
    }
  const reset = () => {
    store.calculator = {
    num1: 0,
    num2: 0,
  },
    store.result = ''
    currentValue.value = ''
    currentOperations.value = ''
    input.value.focus()
  }
  const calculate = () => {
    store.calculator.num2 = +currentValue.value
    currentValue.value = ''
    const {calculator:{num1,num2}} = store
    switch (currentOperations.value) {
        case 'plus':
          store.result = num1 + num2;
          break;
        case 'minus':
          store.result = num1 - num2;
          break;
        case 'multiplication':
          store.result= num1 * num2;
          break;
        case 'division':
          store.result = num1 / num2;
          break;
        default:
          break;
      }
  }
</script>

<template>
  <div>Calculator</div>
  <input ref="input" type="text" v-model="currentValue" />
  <br>
  <br>
  <div class="operations">
    <button :disabled="store.calculator.num1 || !currentValue" @click="setCalcDate('plus')">+</button>
    <button :disabled="store.calculator.num1 || !currentValue" @click="setCalcDate('minus')">-</button>
    <button :disabled="store.calculator.num1 || !currentValue" @click="setCalcDate('multiplication')">*</button>
    <button :disabled="store.calculator.num1 || !currentValue" @click="setCalcDate('division')">/</button>
    <button :disabled="!store.calculator.num1 || !currentValue" @click="calculate">=</button>
    <button @click="reset">Reset</button>
  </div>
</template>

<style scoped>
input {
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #000;
}
</style>



<!--  
    1. Ввод только цифр
    2. Удалить блок operations (функционально оставить возможность через блок кнопок на клавиатуре) // if buttton enter = calculate method // ***if alt+enter = reset method
    3.  
 -->