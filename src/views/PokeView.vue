<script setup>
import { useRoute, useRouter } from 'vue-router';
import {useGetData} from '@/composables/getData';

const router = useRouter();
const route = useRoute();

const {data, getData, loading, errorData} = useGetData();
const back = () => {
    router.push('/pokemons');
};

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
    <p v-if="loading">Cargando informacion...</p>
    <div class="alert alert-danger m-2" v-if="errorData">No existe el pokemon </div>
    <div v-if="data">
        <img :src="data.sprites?.front_default" alt="">
        <h1>Poke name: {{ $route.params.name }}</h1>
    </div>
    <button @click="back" class="btn btn-outline-primary m-2">Volver</button>
</template>