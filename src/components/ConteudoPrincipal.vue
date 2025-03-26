<script setup lang="ts">
import SelecionarIngrediente from './SelecionarIngrediente.vue'
import SuaLista from './SuaLista.vue';
import Rodape from '@/components/Rodape.vue';
import { ref } from 'vue';
import MostrarReceita from './MostrarReceita.vue';


    type Pagina = 'SelecionarIngrediente' | 'MostrarReceitas';
    const ingredientes = ref<string[]>([]);
    const conteudo = ref<Pagina>('SelecionarIngrediente')


    function adicionarNaLista(ingrediente: string){
      ingredientes.value.push(ingrediente);
    }

    function removerIngrediente(ingrediente: string){
      ingredientes.value = ingredientes.value.filter(ing => ing !== ingrediente)
    }

    function navegar(pagina: Pagina){
      console.log('estou navegando');
      
      console.log('pagina: ' + pagina);
      
      conteudo.value = pagina;
      console.log(conteudo.value);
      
    }
  
</script>

<template>
  <main class="conteudo-principal">
    <SuaLista :ingredientes="ingredientes"/>

    <SelecionarIngrediente v-if="conteudo === 'SelecionarIngrediente'"
    @adicionar-ingrediente="adicionarNaLista($event)"
    @remover-ingrediente="removerIngrediente($event)" 
    @buscar-receitas="navegar('MostrarReceitas')"/>

    <MostrarReceita v-else-if="conteudo === 'MostrarReceitas'"/>

  </main>
  <Rodape />
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #fffaf3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

.sua-lista-texto {
  color: var(--coral, #f0633c);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}

.lista-vazia {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.25rem;

  color: var(--coral, #f0633c);
  text-align: center;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>
