<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronoMetro :tempoEmSegundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>Play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>Stop</span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronoMetro from './Cronometro.vue'

export default defineComponent({
    name: "TempoRizador",
    emits: ['aoTemporizadorFinalizado'],
    components: {
        CronoMetro,
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciar() {
            //Começar a contagem
            //1 segundo = 1000 milisegundos
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                //console.log('Incrementando o contador')
                this.tempoEmSegundos += 1
            }, 1000)
            console.log('Iniciando');
        },
        finalizar() {
            this.cronometroRodando = false
            //console.log('Finalizando');
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>