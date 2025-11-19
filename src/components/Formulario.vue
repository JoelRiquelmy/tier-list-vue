<script setup>
    const props = defineProps (['cadastraTarefas', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>
<template>
    
    <form @submit.prevent="props.cadastraTarefas">
    <div class="row">
        <div class="col mb-2">
        <input :value="props.tarefaTemp" @change="evento => props.editaTarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Adicione uma nova tarefa" />
        </div>
        <div class="col-md-1 mb-2">
        <button type="submit" class="btn btn-primary">Adicionar</button>
        </div>
        <div class="col-md-2">
        <select  @change="props.trocarFiltro" class="form-select">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="concluidas">Concluídas</option>
            </select>
        </div>
        </div>
    </form>
</template>