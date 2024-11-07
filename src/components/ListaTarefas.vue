<script setup>
const props = defineProps(['tarefas']);
</script>

<template>
  <div class="list-group mt-4">
    <ul v-if="tarefas.length > 0" class="list-group">
      <li v-for="tarefa in tarefas" :key="tarefa.titulo" class="list-group-item">
        <input
          v-model="tarefa.finalizada"
          :id="`tarefa-${tarefa.titulo}`"
          :name="`tarefa-${tarefa.titulo}`"
          type="checkbox"
        />
        <label
          :class="{ done: tarefa.finalizada }"
          class="ms-3"
          :for="`tarefa-${tarefa.titulo}`"
        >
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
    <div v-else class="alert alert-danger">Não tem mais tarefas pendentes</div>
  </div>
</template>

<style scoped>
.list-group-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 1rem; /* Melhor espaçamento para separar o conteúdo */
  transition: background-color 0.2s;
}

.list-group-item:hover {
  background-color: #f1f1f1; /* Muda a cor do item ao passar o mouse */
}

input[type="checkbox"] {
  transform: scale(1.2); /* Torna o checkbox um pouco maior */
}

.done {
  text-decoration: line-through; /* Linha sobre o texto quando a tarefa está finalizada */
  color: #6c757d; /* Cor cinza para indicar uma tarefa finalizada */
}

.alert-danger {
  text-align: center;
  font-weight: bold;
  margin-top: 1rem;
}
</style>
