<script setup>
import { RouterLink } from 'vue-router';
import { useGetData } from '@/composables/getData';

const { data, getData, loading, errorData } = useGetData();
getData('https://pokeapi.co/api/v2/pokemon');
</script>

<template>
  <div class="pokemon-list-container p-4 my-5">
    <h1 class="title text-center mb-4">Pokémon Directory</h1>

    <p v-if="loading" class="text-muted text-center fs-5">Loading data, please wait...</p>

    <div v-if="errorData" class="alert alert-danger text-center">
      {{ errorData }}
    </div>

    <div v-if="data">
      <div class="row g-3">
        <div
          v-for="poke in data.results"
          :key="poke.name"
          class="col-12 col-sm-6 col-md-4"
        >
          <div class="poke-card p-3 text-center shadow-sm rounded">
            <RouterLink :to="`/pokemons/${poke.name}`" class="poke-link">
              {{ poke.name }}
            </RouterLink>
          </div>
        </div>
      </div>

      <div class="navigation mt-4 d-flex justify-content-center gap-3">
        <button
          :disabled="!data.previous"
          class="btn btn-outline-dark px-4"
          @click="getData(data.previous)"
        >
          ← Previous
        </button>
        <button
          :disabled="!data.next"
          class="btn btn-outline-dark px-4"
          @click="getData(data.next)"
        >
          Next →
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.pokemon-list-container {
  max-width: 1000px;
  margin: 0 auto;
  background-color: #f5f1ec;
  border-radius: 20px;
  box-shadow: 0 0 10px rgba(120, 90, 60, 0.1);
  font-family: 'Segoe UI', sans-serif;
}

.title {
  color: #5c4435;
  font-weight: 600;
}

.poke-card {
  background-color: #fdfaf7;
  transition: background-color 0.3s ease;
  border: 1px solid #e6ddd3;
}

.poke-card:hover {
  background-color: #f1e7dc;
}

.poke-link {
  text-decoration: none;
  font-weight: 500;
  color: #4e3624;
  font-size: 1.1rem;
  text-transform: capitalize;
}

.poke-link:hover {
  color: #7a5e47;
}

.navigation button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-outline-dark {
  border-color: #7a5e47;
  color: #7a5e47;
}

.btn-outline-dark:hover {
  background-color: #7a5e47;
  color: white;
}
</style>
