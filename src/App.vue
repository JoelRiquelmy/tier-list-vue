<script setup>
import { reactive } from 'vue';
import Header from './components/Cabecalho.vue';
import Form from './components/Formulario.vue';
import Lista from './components/Lista.vue';
import Formulario from './components/Formulario.vue';
import Cabecalho from './components/Cabecalho.vue';

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
  <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
  <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.targe.value" :cadastra-tarefas="cadastraTarefa" />
  <Lista :tarefas="getTarefasFiltradas()"/>


</div>
</template>

