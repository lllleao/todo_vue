<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'mudarTarefaTemp', 'setarFiltro'])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.mudarTarefaTemp"
                    required class="form-control" type="text" placeholder="Descrição da tarefa">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.setarFiltro">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="completas">Realizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>