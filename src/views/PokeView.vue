<script setup>
import { useRoute, useRouter } from 'vue-router';
import {useGetData} from '@/composables/getData';
import {useFavoritosStore} from '@/store/favoritos';

const router = useRouter();
const route = useRoute();
const useFavoritos = useFavoritosStore();

const { add, findPoke } = useFavoritos;

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
        <button :disabled="findPoke(data.name)" class="btn btn-primary m-2" @click="add(data)">Agregar a favoritos</button>
    </div>
    <button @click="back" class="btn btn-outline-primary m-2">Volver</button>
</template>