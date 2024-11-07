<script setup>
import { defineEmits, ref } from 'vue';

const emit = defineEmits();

// Variável local para o input da tarefa
const tarefaLocal = ref('');

// Função para cadastro da tarefa
const handleCadastroTarefa = () => {
  if (tarefaLocal.value.trim() !== '') {
    emit('cadastra-tarefa', tarefaLocal.value);
    tarefaLocal.value = ''; // Limpa o input após o envio
  }
};

// Função para trocar o filtro
const handleFilterChange = (event) => {
  emit('trocar-filtro', event.target.value);
};
</script>

<template>
  <form @submit.prevent="handleCadastroTarefa">
    <div class="row">
      <div class="col">
        <input
          v-model="tarefaLocal"
          required
          type="text"
          placeholder="Digite aqui a descrição da tarefa"
          class="form-control"
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="handleFilterChange" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
<style scoped>
form {
  margin-bottom: 1.5rem; /* Espaçamento inferior para separar o formulário da lista */
}

.input {
  border-radius: 0.25rem; /* Arredonda um pouco as bordas do input */
}

button {
  width: 100%;
  background-color: #007bff; /* Cor azul padrão para o botão */
  color: #fff; /* Cor do texto do botão */
  border: none;
  border-radius: 0.25rem;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3; /* Escurece o botão ao passar o mouse */
}
</style>
