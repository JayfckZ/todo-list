<script setup>
const props = defineProps(['filtraTarefa', 'tarefasPendentes', 'filtro'])
</script>

<template>
    {{ console.log(props.tarefasPendentes !== 0) }}
    <ul class="list-group mt-4" v-if="props.tarefasPendentes !== 0 ||props.filtro == 'finalizadas'">
        <li class="list-group-item" v-for="tarefa in props.filtraTarefa">
            <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo"
                type="checkbox" class="me-3">
            <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <h5 class="bg-light mt-2 p-2 text-center rounded 3" v-else>Todas as tarefas foram finalizadas!</h5>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>