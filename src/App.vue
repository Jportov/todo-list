<script setup>
import { reactive, computed } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaTarefas from './components/ListaTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefasTemp: '',
  tarefas: [
    { titulo: 'Estudar Es6', finalizada: false },
    { titulo: 'Estudar SASS', finalizada: false },
    { titulo: 'Ir para a academia', finalizada: true },
  ],
});

const getTarefasPendentes = computed(() => estado.tarefas.filter(tarefa => !tarefa.finalizada));
const getTarefasFinalizadas = computed(() => estado.tarefas.filter(tarefa => tarefa.finalizada));

const getTarefasFiltradas = computed(() => {
  switch (estado.filtro) {
    case 'pendentes':
      return getTarefasPendentes.value;
    case 'finalizadas':
      return getTarefasFinalizadas.value;
    default:
      return estado.tarefas;
  }
});

const cadastraTarefa = (novaTarefa) => {
  const tarefaNova = {
    titulo: novaTarefa,
    finalizada: false,
  };
  estado.tarefas.push(tarefaNova);
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes.length"/>
    <Formulario 
      :trocar-filtro="evento => estado.filtro = evento.target.value" 
      :tarefas-temp="estado.tarefasTemp" 
      :edita-tarefa-temp="evento => estado.tarefasTemp = evento.target.value" 
      :cadastra-tarefa="cadastraTarefa" 
    />
    <ListaTarefas :tarefas="getTarefasFiltradas"/>
  </div>
</template>

