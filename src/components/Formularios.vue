<script setup>
  const props = defineProps(['cadastraTarefa','trocarFiltro','TarefaTemp', 'editarTarefaTemp']);
</script>

<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col">
        <input  required  :value="props.TarefaTemp" @change="props.editarTarefaTemp" 
            type="text" placeholder="Digite sua tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-success">Adicionar +</button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro"  class=" ms-8 form-control form-select">
          <option value="Todas">Tods as tarefas</option>
          <option value="Pendentes">Pendentes</option>
          <option value="Concluidas">Concluidas</option>
        </select>
      </div>
    </div>
  </form>
</template>