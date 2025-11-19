<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-dark text-white rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>