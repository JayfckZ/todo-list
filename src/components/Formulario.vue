<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocaFiltro', 'editaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input required :value="props.tarefaTemp" @change="props.editaTemp" type="text"
                    placeholder="Digite aqui sua tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Registrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocaFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>