<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroNome :tempo-em-segundos="tempoEmSegundos"></CronometroNome>
        <!--Possando tempoEmSegundos para props de Cronometro-->
        <button class="button" @click="iniciar" :disabled="cronometroRodando"> <!--Chamada do método inicar com o evento de clique no botão-->
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando"> <!--Chamada do método finalizar com o evento de clique no botão--> <!--Se o cronometro nao tiver rodando desable = true-->
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import CronometroNome from './Cronometro.vue'

export default defineComponent({
    name: 'TemporizadorNome',
    emits:['aoFinalizarTemporizador'], //lista de eventos que o componente é capaz de emitir
    components:{
        CronometroNome
    },
    data(){ //propriedade, método que retorna um objeto com informaçoes do componente
        return { 
            tempoEmSegundos : 0,
            cronometro : 0, // vai ser o id do intervalo (setInterval)
            cronometroRodando : false
        }
    },
    methods: { // métodos do compontente Formulario
        iniciar(){
            this.cronometroRodando = true
            this.cronometro = setInterval(() =>{
                this.tempoEmSegundos++
            }, 1000) // realizando o primeiro paramentro a cada 1000 ms (1s)
        },
        finalizar(){
            this.cronometroRodando = false
            clearInterval(this.cronometro) // para o intervalo
            this.$emit('aoFinalizarTemporizador', this.tempoEmSegundos) // emits e dados que o evento é capaz de receber
            this.tempoEmSegundos = 0
        }
    }
})
</script>