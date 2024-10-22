<template>
  <div class="container">
    <h1>Calculadora Aritmética</h1>
    <div class="calculadora">
    <div class="numeros">
      <input
        type="number"
        v-model.number="numero1"
        placeholder="Digite um número"
      />
      <input
        type="number"
        v-model.number="numero2"
        placeholder="Digite um número"
      />
    </div>
      <select v-model="operation">
        <option value="+">Adição</option>
        <option value="-">Subtração</option>
        <option value="*">Multiplicação</option>
        <option value="/">Divisão</option>
      </select>
      <div v-if="eNumeroValido(resultado)" class="resultado">
        Resultado: {{ resultado }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const numero1 = ref(0);
const numero2 = ref(0);
const operation = ref('+');

const resultado = computed(() => {
  switch (operation.value) {
    case '+':
      return numero1.value + numero2.value;
    case '-':
      return numero1.value - numero2.value;
    case '*':
      return numero1.value * numero2.value;
    case '/':
      return numero1.value / numero2.value;
    default:
      return 0;
  }
});

const eNumeroValido = (value) => {
  return !isNaN(value) && isFinite(value);
};
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: auto;
  text-align: center;
  .calculadora {
    .numeros{
      display: flex;
      justify-content: space-around;
    }
    select{
      margin: 10px;
      text-align: center;
    }
  }
  .resultado {
    margin-top: 20px;
    font-size: 1.2em;
    font-weight: bold;
  }
}
</style>