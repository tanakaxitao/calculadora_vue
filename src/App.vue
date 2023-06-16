<script setup>
import { reactive } from "vue";

const estado = reactive({
  operacao: "+",
  numero1: 0,
  numero2: 0,
});

const soma = () => {
  return parseInt(estado.numero1) + parseInt(estado.numero2);
};

const subtracao = () => {
  return `${estado.numero1 - estado.numero2}`;
};

const divisao = () => {
  return estado.numero1 / estado.numero2;
};

const multiplicacao = () => {
  return estado.numero1 * estado.numero2;
};

const operacoes = () => {
  const { operacao } = estado;
  switch (operacao) {
    case "+":
      return soma();
    case "-":
      return subtracao();
    case "/":
      return divisao();
    case "*":
      return multiplicacao();
  }
};

const valorPadrao = () => {
  if (estado.numero1 === "") {
    estado.numero1 = 0;
  }
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-black rounded-3">
      <h1 class="text-danger text-center">Calculadora Vue</h1>
    </header>
    <div class="col bg-danger">
      <div class="row w-25 p-3 ms-5 d-inline-flex">
        <input
          type="number"
          @keyup="(evento) => (estado.numero1 = evento.target.value)"
          required
          placeholder="digite um número"
        />
        <input
          type="number"
          @keyup="(evento) => (estado.numero2 = evento.target.value)"
          required
          placeholder="digite um número"
        />
        <span class="fs-2 text-success"
          >Resultado :
          <span v-if="operacoes() >= 0">{{ operacoes() }}</span>
          <span v-else>Preencha os campos</span>
        </span>
      </div>
      <select @change="(evento) => (estado.operacao = evento.target.value)">
        <option value="+">adição</option>
        <option value="-">subtração</option>
        <option value="/">divisão</option>
        <option value="*">multiplicação</option>
      </select>
    </div>
  </div>
</template>

<style scoped></style>
