<template>
    <header>
        <h1>
            <img src="../assets/logo.png" alt="">
        </h1>
        <button class="button" @click="alterarTema">
            {{textoBotao}}
        </button>
    </header>
    
</template>

<script lang="ts">
    import { defineComponent } from 'vue';

    export default defineComponent({ //exportanto o componente com seus dados para ser importado em outro arquivo (App.vue)
        name: 'BarraLateral',
        emits:['aoAlterarTema'],
        data(){
            return{
                modoEscuroAtivo: false
            }
        },
        computed:{
            textoBotao(){
                if(this.modoEscuroAtivo){
                    return 'Ativar modo claro'
                }else{
                    return 'Ativar modo escuro'
                }
            }
        },
        methods:{
            alterarTema(){
                this.modoEscuroAtivo = !this.modoEscuroAtivo
                this.$emit('aoAlterarTema', this.modoEscuroAtivo)
            }
        }
    })
</script>

<style scoped>
    header {
        padding: 1rem;
        background: #0d3b66;
        width: 100%;
        height: 100vh;
        text-align: center;
    }
    @media only screen and (max-width: 768px){
        header{
            padding: 2.5rem;
            height: auto;
        }
    }
</style>