<template>
  <nav class="navbar custom-navbar">
    <div class="container-fluid d-flex justify-content-between align-items-center">
      <router-link class="navbar-brand d-flex align-items-center gap-2" to="/pokemons">
        <img src="@/assets/image.png" alt="Logo" width="80" height="30" />
      </router-link>

      <form
        class="d-flex"
        @submit.prevent="handleSearch"
        v-if="!route.path.includes('/pokemons/') || route.path === '/pokemons'"
      >
        <input
          v-model="searchTerm"
          class="form-control me-2"
          type="search"
          placeholder="Search Pokémon"
        />
        <button class="btn btn-outline-light" type="submit">Search</button>
      </form>
    </div>
  </nav>

  <div class="container text-center mt-4">
    <RouterView />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()
const searchTerm = ref('')

const handleSearch = () => {
  const term = searchTerm.value.trim().toLowerCase()
  if (term) {
    router.push(`/pokemons/${term}`)
    searchTerm.value = ''
  }
}
</script>
