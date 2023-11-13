<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue'
  import Formulario from './components/Formulario.vue'
  import ListaDeTarefas from './components/ListaDeTarefas.vue'

  const estado = reactive({   
    filter: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para a academia',
        finalizada: true,
      },
    ]
   
  }) 
  
     
  const getTarefasPendentes = () => {
       return estado.tarefas.filter(tarefa => !tarefa.finalizada)
    }

    const getTarefasFinalizadas = () => {
       return estado.tarefas.filter(tarefa => tarefa.finalizada)
    }

    const getTarefasFiltradas = () => {
      const { filter } = estado;

      switch (filter) {
        case 'pendentes':
          return getTarefasPendentes();
        case 'finalizadas':
          return getTarefasFinalizadas();
          default: 
          return estado.tarefas
      }
    }

    const cadastrarTarefas = () => {
   
        const tarefaNova = {
          titulo: estado.tarefaTemp,
          finalizada: false,
        }
        estado.tarefas.push(tarefaNova);
        estado.tarefaTemp = '';
        
    }

</script>

<template>
  <div class="container">
    
   <Cabecalho :tarefasPendentes="getTarefasPendentes().length"/>
   <Formulario :trocarFiltro="evento => estado.filter = evento.target.value" :editaTarefa-Temp="evento => estado.tarefaTemp = evento.target.value" :cadastraTarefa="cadastrarTarefas" />
   <ListaDeTarefas :tarefas="getTarefasFiltradas()" /> 
   
  </div>
</template>

