<script setup>
import { computed } from "vue";

const props = defineProps(["pokemon"]);

const pokemonImage = computed(
  () =>
    `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${props.pokemon.id}.png`
);
</script>

<template>
  <div class="pokemon-item">
    <div class="pokemon-id">#{{ pokemon.id }}</div>
    <img :src="pokemonImage" :alt="pokemon.name" class="pokemon-image" />
    <div class="pokemon-name">{{ pokemon.name }}</div>

    <div class="pokemon-types">
      <span
        v-for="type in pokemonTypes"
        :key="type.name"
        class="pokemon-type"
        :style="{ backgroundColor: type.color }"
      >
        {{ type.name }}
      </span>
    </div>
  </div>
</template>

<style scoped>
.pokemon-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 16%;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-transform: capitalize;
  transition: 0.3s;
}

.pokemon-item:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.pokemon-image {
  width: 100px;
  height: 100px;
}

.pokemon-name {
  font-weight: bold;
  font-size: 16px;
  margin-top: 10px;
}

.pokemon-types {
  display: flex;
  gap: 5px;
  margin-top: 10px;
}

.pokemon-type {
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 14px;
  color: white;
}
</style>
