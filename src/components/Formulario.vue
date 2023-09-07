<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulario para criacao de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa voce deseja iniciar?" v-model="descricao">
                <!--v-model linka os dados com a descriçao do input , desricao recebe o que esta escrito no input-->
            </div>
            <div class="column">
                <TemporizadorNome @ao-finalizar-temporizador="finalizarTarefa"/>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TemporizadorNome from './Temporizador.vue';

export default defineComponent({
    name: 'FormularioNome',
    emits: ['aoSalvarTarefa'],
    components: {
        TemporizadorNome
    },
    data() {
        return {
            descricao: ''
        }
    },
    methods: {
        finalizarTarefa(tempoEmSegundos: number): void {
            this.$emit('aoSalvarTarefa',{
                duracaoEmSegundos: tempoEmSegundos,
                descricao: this.descricao
            })
            this.descricao = ''

        }
    }
})
</script>

<style>
.formulario{
    color: var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>
