<script setup>
const props = defineProps(['filtrar'])
</script>

<template>
    <div v-if="props.filtrar.length > 0">
        <ul class="list-group mt-4">
            <li class="list-group-item mb-3 shadow-sm" v-for="tarefa in props.filtrar">
                <input @change="item => tarefa.finalizada = item.target.checked" :checked="tarefa.finalizada"
                    type="checkbox" :id="tarefa.titulo">
                <label :for="tarefa.titulo" :class="{ done: tarefa.finalizada }" class="ms-3">{{ tarefa.titulo
                    }}</label>
            </li>
        </ul>
    </div>
    <div v-else class="sem-tarefas col-3 mt-4 fs-5 p-2 text-center">
        Não esxiste tarefa pendente.
    </div>
</template>
<style scoped>
.done {
    text-decoration: line-through;
}

label,
input {
    cursor: pointer;
}

.sem-tarefas {
    background-color: rgb(58, 179, 58);
    color: #fff;
}
</style>
