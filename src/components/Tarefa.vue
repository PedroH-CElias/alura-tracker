<template>
    <BoxNome>
        <div class="columns">
            <div class="column is-7">
                {{tarefa.descricao || 'Tarefa sem descrição'}}
            </div>
            <div class="column">
                <CronometroNome :tempo-em-segundos="tarefa.duracaoEmSegundos"></CronometroNome>
            </div>
        </div>
    </BoxNome>
</template>

<script lang="ts">
import { defineComponent,PropType } from 'vue';
import CronometroNome from './Cronometro.vue';
import ITarefa from '../interfaces/ITarefa';
import BoxNome from './Box.vue';


export default defineComponent({
    name: 'TarefaNome',
    components:{
    CronometroNome,
    BoxNome
},
    props:{
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true    
        }
    }
})
</script>
