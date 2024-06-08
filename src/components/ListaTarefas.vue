<script setup>
const props = defineProps(['tarefas']);
</script>

<template>
<div class="list-group mt-4">
    <ul v-if="props.tarefas.length > 0" class="list-group">
    <li v-for="tarefa in props.tarefas" :key="tarefa.titulo" class="list-group-item">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
    </li>
    </ul>
    <div v-else class="alert alert-danger">Não tem mais tarefas pendentes</div>
</div>
</template>

<style scoped>
.done {
text-decoration: line-through;
}
</style>
