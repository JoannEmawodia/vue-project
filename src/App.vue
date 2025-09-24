<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import Lista from './components/Lista.vue';

  const estado = reactive ({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo:'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para a academia',
        finalizada: true,
      }
    ]
  })

  const getTarefaPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefaFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () =>{
    const filtro = estado.filtro;

    switch (filtro){
      case 'pendentes':
        return getTarefaPendentes();
      case 'finalizadas':
        return getTarefaFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () =>{
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '';
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefa-pendentes="getTarefaPendentes().length" />
    <Formulario :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp=evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento =>estado.filtro= evento.target.value" />
    <Lista :tarefas="getTarefasFiltradas()" />
  </div>
</template>


