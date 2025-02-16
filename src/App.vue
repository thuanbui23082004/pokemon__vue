<script setup>
import PokemonList from "./components/PokemonList.vue";
</script>

<template>
  <div class="container">
    <h1 class="title">Pokémon API</h1>
    <PokemonList />
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  margin-block: 50px;
  font-size: 15px;
  color: #2c3e50;
}
.title {
  text-align: center;
  margin-bottom: 50px;
  font-weight: 400;
}
</style>
