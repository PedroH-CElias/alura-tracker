<template>
    <section>
        <strong class="display">
            <!--capturar dados do vue-->
            {{ tempoDecorrido }}
        </strong>
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'CronometroNome',
    props:{ //propriedades que vamos receber nesse componente
        tempoEmSegundos : { //nome da propriedade, recebe a partir do uso do componente em outro
            type : Number, // tipo
            default: 0 // valor padrão
        }
    },
    computed:{
        tempoDecorrido() : string {
            return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11,8) // formatando a forma como o tempo vai aparecer em 00:00:00
        }
    }
})

</script>

<style>
.display{
    color: var(--texto-primario);
}
</style>