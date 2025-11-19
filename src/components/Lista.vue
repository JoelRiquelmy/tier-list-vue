<script setup>
const props = defineProps (['tarefas'])
</script>

<template>
    <p v-if="props.tarefas.length === 0">
        Nenhuma tarefa {{ props.tarefas.length === 0 ? 'pendente' : 'concluída' }}.
    </p>
    <ul class="list-group mt-4" v-else>
        <li class="list-group-item" v-for="tarefa in props.tarefas">
        <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" type="checkbox" name="" :id="tarefa.id" />
        <label :class="{done: tarefa.concluida }" class="ms-3" :for="tarefa.id">
            {{ tarefa.descricao }}
        </label>
        </li>
    </ul>
</template>

<style scoped>

.done {
    text-decoration: line-through;
    color: gray;
}
</style>