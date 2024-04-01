<script setup>
import { reactive } from 'vue';

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
    <header>
      <h1>Minnhas tarefas</h1>
      <p class="p-5 mt-4 mb-4 bg-light rounded-3">
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes.
      </p>

    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="e => estado.tarefaTemp = e.target.value" type="text" placeholder="Digite aqui sua tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Registrar</button>
        </div>
        <div class="col-md-2">
          <select @change="e => estado.filtro = e.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
        <ul class="list-group mt-4">
          <li class="list-group-item" v-for="tarefa in getTarefaFiltrada()">
            <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" class="me-3">
            <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
              {{ tarefa.titulo }}
            </label>
          </li>
        </ul>
      </div>
      
    </form>
  </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
