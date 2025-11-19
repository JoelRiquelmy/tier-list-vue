<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { id: 1, descricao: 'Estudar Vue.js', concluida: false },
    { id: 2, descricao: 'Fazer compras', concluida: true },
    { id: 3, descricao: 'Ler um livro', concluida: false },
    { id: 4, descricao: 'Exercitar-se', concluida: false },
    { id: 5, descricao: 'Cozinhar jantar', concluida: true },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.concluida);
};

const getTarefasConcluidas = () => {
  return estado.tarefas.filter(tarefa => tarefa.concluida);
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes': 
      return getTarefasPendentes();
    case 'concluidas': 
      return getTarefasConcluidas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    descricao: estado.tarefaTemp,
    concluida: false,
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemp = ''
}
</script>

<template>
<div class="container">
  <header class="p-5 mb-4 mt-4 bg-dark text-white rounded-3">
    <h1>Minhas tarefas</h1>
    <p>
      você possui {{ getTarefasPendentes().length }} tarefas pendentes
    </p>
  </header>

  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col mb-2">
        <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Adicione uma nova tarefa" />
      </div>
      <div class="col-md-1 mb-2">
        <button type="submit" class="btn btn-primary">Adicionar</button>
      </div>
      <div class="col-md-2">
        <select  @change="evento => estado.filtro = evento.target.value" class="form-select">
          <option value="todas">Todas</option>
          <option value="pendentes">Pendentes</option>
          <option value="concluidas">Concluídas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" type="checkbox" name="" :id="tarefa.id" />
      <label :class="{done: tarefa.concluida }" class="ms-3" :for="tarefa.id">
        {{ tarefa.descricao }}
      </label>
    </li>
  </ul>
</div>
</template>

<style scoped>
.container {
  max-width: 600px;
}

.done {
  text-decoration: line-through;
  color: gray;
}
</style>
