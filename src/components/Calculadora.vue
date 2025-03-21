<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
  n1: 0,
  n2: 0,
  operacao: "+",
});

const operacoes = [
  {label: "+", value: "+" },
  {label: "-", value: "-" },
  {label: "x", value: "*" },
  {label: "÷", value: "/" },
];


function calculaResultado() {
  if (estado.operacao === "/") {
    
    if (estado.n2 === 0) {
      if(estado.n2 === 0) {
        return "indefinido";
      } else {
        return "Não pode dividir por zero";
      }
    }
  }

  if (estado.operacao === "*") {
    if( estado.n1 === 0 || estado.n2 === 0) {
      return "Multiplicação por zero";
    } 
  }

  switch (estado.operacao) {
    case "+":
      return estado.n1 + estado.n2;
    case "-":
      return estado.n1 - estado.n2;
    case "*":
      return estado.n1 * estado.n2;
    case "/":
      return estado.num2 !== 0 ? estado.n1 / estado.n2 : "erro";
    default:
      return 0;  
  }
}

</script>


<template>
    <form>
      <div class="row align-items-end">
        <div class="col-md-4">
          <label for="campo1">Número 1</label>
          <input v-model="estado.n1" class="form-control" type="number"  id="campo1">
        </div>

        <div class="col-md-4">
          <select v-model="estado.operacao" class="form-control text-center">
            <option v-for="op in operacoes" :key="op.value" :value="op.value" value="+">
              {{ op.label }}
            </option>
          </select>
        </div>

        <div class="col-md-4">
          <label for="campo2">Número 2</label>
          <input v-model="estado.n2" class="form-control" type="number" id="campo2">
        </div>
        <div class="m-3 bg-light text-center">
          <h3>Resultado: {{ calculaResultado() }}</h3>        
        </div>
      </div>
    </form>
</template>