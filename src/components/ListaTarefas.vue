<script setup>
  const props = defineProps(['tarefas']);
</script>

<template>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input  @change=" evento => tarefa.Concluidas = evento.target.checked " :checked="tarefa.Concluidas" :id="tarefa.titulo" type="checkbox" class="form-check-input" >
      <label  :class="{done: tarefa.Concluidas === true}" class="ms-3" :for="tarefa.texto">
        {{tarefa.titulo}}
      </label>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>