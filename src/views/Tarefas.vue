<template>
    <FormuLário @aoSalvarTarefa="salvarTarefa" />
    <div class="lista">
        <TareFa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <Box v-if="listaEstaVazia">
            Você não está muito produtivo hoje :(
        </Box>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FormuLário from '../components/Formulario.vue'
import TareFa from '../components/Tarefa.vue'
import ITarefa from '../Interfaces/ITarefa'
import Box from '../components/Box.vue'

export default defineComponent({
    name: 'App',
    components: {
        FormuLário,
        TareFa,
        Box
    },
    data() {
        return {
            tarefas: [] as ITarefa[],
        }
    },
    computed: {
        listaEstaVazia(): boolean {
            return this.tarefas.length === 0
        }
    },
    methods: {
        salvarTarefa(tarefa: ITarefa) {
            this.tarefas.push(tarefa)
        }
    }
});
</script>

