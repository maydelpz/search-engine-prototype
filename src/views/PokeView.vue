<script setup>
import { useRoute, useRouter } from 'vue-router';
import { useGetData } from '@/composables/getData';

const router = useRouter();
const route = useRoute();

const { data, getData, loading, errorData } = useGetData();

const back = () => {
  router.push('/pokemons');
};

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
  <div class="detail-container text-center p-4 my-5">
    <div v-if="loading" class="text-muted fs-4">Loading Pokémon data...</div>

    <div v-if="errorData" class="alert alert-danger my-3"> 
      Pokémon not found.
    </div>

    <div v-if="data" class="poke-detail card shadow-sm p-4 mx-auto">
      <img
        :src="data.sprites?.front_default"
        alt="Pokemon image"
        class="pokemon-img mx-auto mb-3"
      />
      <h2 class="card-title text-capitalize mb-3">{{ $route.params.name }}</h2>
      
      <div class="info text-start">
        <p><strong>Height:</strong> {{ data.height / 10 }} m</p>
        <p><strong>Weight:</strong> {{ data.weight / 10 }} kg</p>
        <p><strong>Base Experience:</strong> {{ data.base_experience }}</p>

        <h5 class="mt-4">Abilities</h5>
        <ul class="list-group rounded mt-2">
          <li
            v-for="ability in data.abilities"
            :key="ability.ability.name"
            class="list-group-item text-capitalize"
          >
            {{ ability.ability.name }}
          </li>
        </ul>
      </div>
    </div>

    <button @click="back" class="btn btn-outline-dark mt-4 px-4">
      Go Back
    </button>
  </div>
</template>

<style scoped>
.detail-container {
  max-width: 700px;
  margin: 0 auto;
  background-color: #f5f1ec;
  border-radius: 20px;
  font-family: 'Segoe UI', sans-serif;
  box-shadow: 0 0 12px rgba(120, 90, 60, 0.1);
}

.poke-detail {
  background-color: #fdfaf7;
  border-radius: 15px;
  max-width: 450px;
  border: 1px solid #e6ddd3;
}

.pokemon-img {
  width: 150px;
  height: auto;
  background-color: #f1e7dc;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 2px 8px rgba(120, 90, 60, 0.1);
}

.card-title {
  color: #5c4435;
  font-weight: 600;
  font-size: 1.6rem;
}

.info p {
  margin: 0.3rem 0;
  color: #6b4f3b;
}

ul.list-group {
  background-color: transparent;
}

ul.list-group li {
  background-color: #f7efe7;
  border: none;
  color: #4e3624;
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
