<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue'
  import Formulario from './components/Formulario.vue'
  import Tarefas from './components/Tarefas.vue'

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar',
        finalizada: true
      },
      {
        titulo: 'Ir ao mercado',
        finalizada: false
      },
      {
        titulo: 'Ir para a academa',
        finalizada: false
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefaFiltrada = () => {
    const {filtro} = estado

    switch(filtro){
      case 'pendentes':
        return getTarefasPendentes()
      case 'finalizadas':
        return getTarefasFinalizadas()
      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const novaTarefa = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }

    estado.tarefas.push(novaTarefa)
    estado.tarefaTemp = ''
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :cadastra-tarefa="cadastraTarefa" :tarefa-temp="estado.tarefaTemp" :troca-filtro="(e) => estado.filtro = e.target.value" :edita-temp="(e) => estado.tarefaTemp = e.target.value" />
    <Tarefas :filtra-tarefa="getTarefaFiltrada()" :tarefas-pendentes="getTarefasPendentes().length" :filtro="estado.filtro"/>
  </div>
</template>
