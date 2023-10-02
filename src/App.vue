<script setup>
import { reactive } from 'vue';
import Header from './components/Header.vue';
import Formularios from './components/Formularios.vue'
import ListaTarefas from './components/ListaTarefas.vue';



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
  const { filtro } = estado;

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
  const TarefaNova = {
    titulo: estado.TarefaTemp,
    Concluidas: false
  }

  estado.tarefas.push(TarefaNova);
  estado.TarefaTemp = '';
};

</script>

<template>
  <div class="container">
      <Header :tarefasPendentes="getTarefasPendentes().length"></Header>
      <Formularios :trocarFiltro="evento => estado.filtro = evento.target.value" :TarefaTemp="estado.TarefaTemp" :editarTarefaTemp="evento => estado.TarefaTemp = evento.target.value" :cadastraTarefa="cadastraTarefa" ></Formularios>
      <ListaTarefas :tarefas="getTarefasFiltradas()"></ListaTarefas>
  </div>
</template>


