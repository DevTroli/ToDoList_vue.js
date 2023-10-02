<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'Todas', 'Pendentes': true, 'Concluidas': true,
    TarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar vueJs',
        Concluidas: false
      },

      {
        titulo: 'Estudar Inglês',
        Concluidas: true
      },

      {
        titulo: 'Estudar React',
        Concluidas: false
      },

      {
        titulo: 'Estudar Next.js',
        Concluidas: false
      }

    ]
  })
  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.Concluidas);
  }
  const getTarefasconcluidas = () => {
    return estado.tarefas.filter(tarefa => tarefa.Concluidas);
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'concluidas':
        return getTarefasconcluidas();
      default:
        return estado.tarefas;
        }
  }

  const cadastraTarefa = () => {
    const  TarefaNova = {
      titulo: estado.TarefaTemp,
      Concluidas: false
      }

      estado.tarefas.push(TarefaNova);
      estado.TarefaTemp = '';
    };
  
</script>

<template>
<div class="container">
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>
      minhas tarefas
    </h1>
    <p>
      Você tem {{ getTarefasPendentes().length }} tarefas pendentes!!
    </p>
  </header>
  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input @change="evento => estado.TarefaTemp = evento.target.value" required type="text" placeholder="Digite sua tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-success">Adicionar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value"  class=" ms-8 form-control form-select">
          <option value="Todas">Tods as tarefas</option>
          <option value="Pendentes">Pendentes</option>
          <option value="Concluidas">Concluidas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input  @change=" evento => tarefa.Concluidas = evento.target.checked " :checked="tarefa.Concluidas" :id="tarefa.titulo" type="checkbox" class="form-check-input" >
      <label  :class="{done: tarefa.Concluidas === true}" class="ms-3" :for="tarefa.texto">
        {{tarefa.titulo}}
      </label>
    </li>

  </ul>
</div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
