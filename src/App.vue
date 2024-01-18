<script setup>
  import { reactive } from 'vue';

  const estadoApp = reactive({
    resultado: 0,
    algaritmo1: null,
    algaritmo2: null,    
    options: [
        { value: 0, label: 'Selecione um operação' },
        { value: 1, label: 'Soma' },
        { value: 2, label: 'Subtração' },
        { value: 3, label: 'Multiplicação' },
        { value: 4, label: 'Divisão' }
      ],
    selectedOption: 0
  })

  function calcular (){    
    if(estadoApp.selectedOption != 0){
      document.getElementById('alertaOperador').classList.add('remove-alert')
      switch(estadoApp.selectedOption){
        case 1:           
          estadoApp.resultado = estadoApp.algaritmo1 + estadoApp.algaritmo2;
        break;
        case 2:
          estadoApp.resultado = estadoApp.algaritmo1 - estadoApp.algaritmo2;
        break;
        case 3:
          estadoApp.resultado = estadoApp.algaritmo1 * estadoApp.algaritmo2;
        break;
        case 4:
          estadoApp.resultado = estadoApp.algaritmo1 / estadoApp.algaritmo2;
        break;
        default:
          console.log('estado da opcao: '+estadoApp.opcao)          
      }      
    } else {
      document.getElementById('alertaOperador').classList.remove('remove-alert')
      estadoApp.algaritmo1 = null;
      estadoApp.algaritmo2 = null;
    }
  }

</script>

<template>
  
  <div class="container">
    <div id="alertaOperador" class="alert alert-info" role="alert">
      Selecione uma operação antes de inserir os valores nos campos solitados.
    </div>
    <div class="card">
      <h5 class="card-header text-center"><i class="bi bi-calculator"></i> Calculadora</h5>
      <div class="card-body">
        <div class="input-group mb-3">
          <span class="input-group-text" id="inputGroup-sizing-default">Primeiro número</span>
          <input v-model.number="estadoApp.algaritmo1" type="number" class="form-control" @change="calcular()" />
        </div>
        <div class="input-group mb-3">
          <span class="input-group-text" id="inputGroup-sizing-default">Segundo número</span>
          <input v-model.number="estadoApp.algaritmo2" type="number" class="form-control" @change="calcular()" />
        </div>  

        <div class="input-group mb-3">         
          <label class="input-group-text" for="operacaoId">Operação</label>
          <select v-model="estadoApp.selectedOption" @change="calcular()" class="form-select" id="operacaoId">
            <option v-for="option in estadoApp.options" :value="option.value">
              {{ option.label }}
            </option>
          </select>
        </div>
      </div>
      <div class="card-footer text-center" v-if="estadoApp.selectedOption != 0 && estadoApp.selectedOption != null">
        <p class="badge bg-primary text-wrap fs-3">Resultado: {{ estadoApp.resultado }}</p> 
      </div>
      <div class="card-footer">
        <p class="text-body-secondary">
          Selecione uma operação para iniciar, visite a <a href="https://github.com/gbri-dev/calculadora-vue" target="_blank" class="text-reset">documentação</a>.
        </p>
      </div>
    </div>
  </div>  
</template>

<style>
/* .container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
} */

.container {
  margin-top: 10%;
}

.remove-alert {
  display: none;
}

</style>
