<script setup>
  import { computed, reactive } from 'vue';

  const estado = reactive({
  n1: "",
  n2: "",
  operacao: "+",
});

const operacoes = [
  {label: "+", value: "+" },
  {label: "-", value: "-" },
  {label: "x", value: "*" },
  {label: "÷", value: "/" },
];




const onChange = (campo) => {
 
  estado[campo] = estado[campo].replace(/[^0-9.-]/g, '');
};


const resultado = computed(() => {
  
  if (!estado.n1 || !estado.n2 || !estado.operacao) return '';

  const n1 = parseFloat(estado.n1);
  const n2 = parseFloat(estado.n2);

  if (isNaN(n1) || isNaN(n2)) return 'Insira números válidos';

 
  if (estado.operacao === '/' && n2 === 0) return 'Não pode dividir por zero';

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
})

</script>


<template>
    <form class="text-center">
      <div class="row align-items-end">
        <div class="col-md-4">
          <label for="campo1">Número 1</label>
          <input v-model="estado.n1" class="form-control text-center" type="number"  id="campo1">
        </div>

        <div class="col-md-4">
          <label for="">Operador</label>
          <select v-model="estado.operacao" class="form-control text-center">
            <option v-for="op in operacoes" :key="op.value" :value="op.value" value="+">
              {{ op.label }}
            </option>
          </select>
        </div>

        <div class="col-md-4">
          <label for="campo2">Número 2</label>
          <input v-model="estado.n2" class="form-control text-center" type="number" id="campo2">
        </div>
        <div class="m-3 bg-light text-center">
          <h3>O resultado é: {{ resultado }}</h3>        
        </div>
      </div>
    </form>
</template>