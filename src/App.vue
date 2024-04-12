<script setup>
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import Todo from './components/Todo.vue';
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

const cadastrarTarefa = () => {
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
    <Cabecalho :tarefas-pendentes="pendentesTarefa().length" />
    <Formulario :tarefa-temp="estado.tarefaTemporaria" :cadastrar-tarefa="cadastrarTarefa" :mudar-tarefa-temp="item => estado.tarefaTemporaria = item.target.value" :setar-filtro="setarFiltro" />
    <Todo :filtrar="filtrar()"/>
  </div>
</template>

