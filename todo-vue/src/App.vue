<script setup>
import { reactive } from 'vue';

  const estado = reactive({
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

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui 7 tarefas pendentes!
      </p>
    </header>
  </div>
  <form>
      <div class="row">
        <div class="col">
          <input type="text" placeholder="Digite aqui as descrição da tarefa" class="form-control">
        </div>     
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control">
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in estado.tarefas">
        <input :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
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
