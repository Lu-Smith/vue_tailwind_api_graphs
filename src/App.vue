<script setup lang="ts">
  import { ref } from 'vue';
  import GraphGrids from './components/GraphGrids.vue';
  import Header from './components/Header.vue';
  import Footer from './components/Footer.vue';
  import axios from "axios";

  const pokemonName = ref('ditto');

  const URL = `https://pokeapi.co/api/v2/pokemon/${pokemonName}`;

  const getPokemon = async () => {
    const respnse = await URL.get();
    return respnse.data;
  }

</script>

<template>
  <Header :pokemonName="pokemonName" />
  <form action="">
    <input type="text" placeholder="Choose your pokemon" :value="pokemonName" />
  </form>
  <GraphGrids :pokemonName="pokemonName" />
  <Footer />
</template>

<style scoped>

</style>
