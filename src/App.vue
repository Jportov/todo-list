<script setup>
import { computed, reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaTarefas from './components/ListaTarefas.vue';

// Estado global para armazenar tarefas e filtro
const estado = reactive({
  filtro: 'todas',
  tarefas: [
    { titulo: 'Estudar ES6', finalizada: false },
    { titulo: 'Estudar SASS', finalizada: false },
    { titulo: 'Ir para a academia', finalizada: true },
  ],
});

// Computed para obter as tarefas filtradas
const getTarefasFiltradas = computed(() => {
  switch (estado.filtro) {
    case 'pendentes':
      return estado.tarefas.filter(tarefa => !tarefa.finalizada);
    case 'finalizadas':
      return estado.tarefas.filter(tarefa => tarefa.finalizada);
    default:
      return estado.tarefas;
  }
});

// Função para cadastrar uma nova tarefa
const cadastraTarefa = (novaTarefa) => {
  if (novaTarefa.trim() !== '') {
    estado.tarefas.push({ titulo: novaTarefa, finalizada: false });
  }
};

// Função para trocar o filtro
const trocarFiltro = (novoFiltro) => {
  estado.filtro = novoFiltro;
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="estado.tarefas.filter(tarefa => !tarefa.finalizada).length" />
    <Formulario @cadastra-tarefa="cadastraTarefa" @trocar-filtro="trocarFiltro" />
    <ListaTarefas :tarefas="getTarefasFiltradas" />
  </div>
</template>
<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto; /* Centraliza o conteúdo horizontalmente */
  padding-top: 2rem; /* Espaçamento superior para melhorar a visualização */
}
</style>