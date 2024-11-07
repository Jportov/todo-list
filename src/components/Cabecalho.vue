<script setup>
const props = defineProps(['tarefasPendentes']);
</script>

<template>
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minhas tarefas</h1>
    <p>Você possui {{ tarefasPendentes }} tarefas pendentes!</p>
  </header>
</template>

<style scoped>
header {
  background-color: #f8f9fa; /* Cor clara para destacar o cabeçalho */
  text-align: center;
}

h1 {
  font-size: 2rem;
  color: #343a40; /* Cor escura para o título */
}

p {
  font-size: 1.25rem;
  color: #6c757d; /* Cor cinza para indicar quantidade de tarefas pendentes */
}
</style>

