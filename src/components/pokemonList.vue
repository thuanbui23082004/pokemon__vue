<script setup>
import { ref, computed, onMounted } from "vue";
import PokemonItem from "./PokemonItem.vue";

const fetchAPI = async (url) => {
  const response = await fetch(url);
  const data = await response.json();
  return data;
};

function getIDPokemon(url) {
  const parts = url.split("/");
  return parseInt(parts[parts.length - 2], 10);
}

const pokemons = ref([]);
const filteredPokemons = ref([]);
const offset = ref(0);
const NUMBER_OF_RENDER = 20;

async function getPokemon() {
  const data = await fetchAPI("https://pokeapi.co/api/v2/pokemon/?offset=0&limit=898");
  pokemons.valunpe = data.results.map((item) => ({
    id: getIDPokemon(item.url),
    name: item.name,
  }));
  filteredPokemons.value = pokemons.value;
}

onMounted(getPokemon);

const renderPokemons = computed(() =>
  filteredPokemons.value.slice(0, offset.value + NUMBER_OF_RENDER)
);

function handleLoadmore() {
  offset.value += NUMBER_OF_RENDER;
}

function handleSearch(event) {
  filteredPokemons.value = pokemons.value.filter((pokemon) =>
    pokemon.name.includes(event.target.value.toLowerCase())
  );
  offset.value = 0;
}
</script>

<template>
  <div class="pokemon-list-container">
    <div class="search-bar">
      <input type="text" placeholder="Search Pokémon..." @input="handleSearch" />
    </div>

    <div class="pokemon-list">
      <PokemonItem v-for="pokemon in renderPokemons" :key="pokemon.id" :pokemon="pokemon" />
    </div>

    <button
      v-show="filteredPokemons.length > NUMBER_OF_RENDER"
      class="load-more"
      @click="handleLoadmore"
    >
      Load More
    </button>
  </div>
</template>

<style scoped>
.search-bar {
  display: flex;
  justify-content: center;
  margin: 0 15px 50px;
}

.search-bar input {
  max-width: 300px;
  width: 100vw;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 16px;
  margin-bottom: 20px;
}

.pokemon-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
}

.load-more {
  display: block;
  margin-top: 50px;
  margin-inline: auto;
  padding: 10px 20px;
  font-size: 16px;
  background-color: #ff4d4f;
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.load-more:hover {
  opacity: 0.9;
}
</style>
