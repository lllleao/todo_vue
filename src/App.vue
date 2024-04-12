<script setup>
import { reactive } from 'vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemporaria: '',
  tarefas: [
    {
      titulo: 'Estudar',
      finalizada: false
    },
    {
      titulo: 'Arrumar o quarto',
      finalizada: false
    },
    {
      titulo: 'Ler quadrinho',
      finalizada: true
    }
  ]

})

const pendentesTarefa = () => {
  return estado.tarefas.filter(item => {
    return !item.finalizada
  })
}

const realizadaTarefas = () => {
  return estado.tarefas.filter(item => {
    return item.finalizada
  })
}

function setarFiltro(elemento) {
  estado.filtro = elemento.target.value

}

function filtrar() {
  const {filtro} = estado

  switch (filtro) {
    case 'pendentes':
      return pendentesTarefa()
    case 'completas':
      return realizadaTarefas()
    default:
      return estado.tarefas
  }
}

const cadastrarTarefa = (elemento) => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }
  
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemporaria = ''
}

</script>



<template>
  <div class="container">
    <header class="text-center p-5 mb-4 mt-4 bg-blue rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ pendentesTarefa().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria" @change="item => estado.tarefaTemporaria = item.target.value" required class="form-control" type="text" placeholder="Descrição da tarefa">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="setarFiltro">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="completas">Realizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item mb-3 shadow-sm" v-for="tarefa in filtrar()">
        <input @change="item => tarefa.finalizada = item.target.checked" :checked="tarefa.finalizada" type="checkbox" :id="tarefa.titulo">
        <label :for="tarefa.titulo" :class="{ done: tarefa.finalizada }" class="ms-3">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

label, input {
  cursor: pointer;
}
</style>
