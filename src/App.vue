<template>
  <main class="columns is-gapless is-multiline " :class="{'modo-escuro': modoEscuroAtivo}">
    <div class="column is-one-quarter">
      <BarraLateral @aoAlterarTema="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioNome @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <!--Lista de Tarefas-->
        <!--v-for = para cada....-->
        <!--Index eh a posicao do item na lista, para poder ser usada como chave primaria -->
        <TarefaNome v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <Box v-if="listaEstaVazia">
          <p>Você não está muito produtivo hoje :(</p>
        </Box>
      </div>
    </div>
  </main>
</template>


<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue' // importando o componente BarraLateral
import FormularioNome from './components/Formulario.vue'
import TarefaNome from './components/Tarefa.vue';
import ITarefa from './interfaces/ITarefa'
import Box from './components/Box.vue';

export default defineComponent({
  name: 'App',
  //Compondo o componente com outros componentes, mostrar quais componente fazem parte desse
  components: {
    BarraLateral,
    FormularioNome,
    TarefaNome,
    Box
  },
  data() { // estado de um componente
    return {
      tarefas: [] as ITarefa[], // array de tarefas
      modoEscuroAtivo: false
    }
  },
  computed:{
    listaEstaVazia() : boolean{
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema(modoEscuroAtivo : boolean){
          this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
.lista {
  padding: 1.5rem;
}
p {
  text-align: center;
}
main{
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro{
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>
