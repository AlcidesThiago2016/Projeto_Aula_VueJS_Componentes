<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizado: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizado: false,
      },
      {
        titulo: 'Ir para academia',
        finalizado: true,
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizado);
  }
  
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado);
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastrarTarefa = (e) => {
    e.preventDefault()
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizado: false,
    }
    estado.tarefas.push(tarefaNova);
  }


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes!
      </p>
    </header>
  </div>
  <form @submit="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui as descrição da tarefa" class="form-control">
        </div>     
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
