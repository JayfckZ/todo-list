<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header>
        <h1 class="mt-4">Minhas tarefas</h1>
        <p class="p-5 mt-4 mb-4 bg-light rounded-3">
            Você possui {{ props.tarefasPendentes }} tarefas pendentes.
        </p>
    </header>
</template>