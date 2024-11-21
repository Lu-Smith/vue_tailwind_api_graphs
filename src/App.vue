<script setup lang="ts">
  import { ref, computed, onMounted, watch } from 'vue';
  import GraphGrids from './components/GraphGrids.vue';
  import Header from './components/Header.vue';
  import Footer from './components/Footer.vue';
  import axios from "axios";

  const pokemonName = ref('ditto');

  const pokemonData = ref(null);

  const URL = computed(() => `https://pokeapi.co/api/v2/pokemon/${pokemonName.value}`);

  const fetchPokemonData = async () => {
    try {
      const respnse = await axios.get(URL.value);
      pokemonData.value = respnse.data;
      console.log("Fetched Pokémon:", pokemonData.value);
    } catch (err) {
      console.console.error("Error fetching Pokemon data: ", err);
      pokemonData.value = null;
    }
  };

  onMounted(() => {
    fetchPokemonData();
  }),

  watch(pokemonName, fetchPokemonData);

</script>

<template>
  <Header :pokemonName="pokemonName" />
  <form @submit.prevent="fetchPokemonDAta">
    <input type="text" placeholder="Choose your pokemon.." :v-model="pokemonName" />
    <button type="submit">Submit</button>
  </form>
  <p>{{ pokemonName }}</p>
  <GraphGrids :pokemonName="pokemonName" />
  <Footer />
</template>
