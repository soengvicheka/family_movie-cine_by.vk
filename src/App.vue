<template>
  <div class="site-shell">
    <header class="site-header">
      <router-link class="brand" to="/" aria-label="MovieCine home">
        <span class="brand-mark">MC</span>
        <span>
          <strong>MovieCine</strong>
          <small>Family movie finder</small>
        </span>
      </router-link>

      <form class="search-bar" @submit.prevent="submitSearch">
        <input
          v-model.trim="searchText"
          type="search"
          placeholder="Find a movie..."
          aria-label="Search movies"
        />
        <button type="submit">Search</button>
      </form>

      <nav class="site-nav" aria-label="Movie genres">
        <router-link
          v-for="genre in genres"
          :key="genre"
          :to="`/genre/${genre}`"
        >
          {{ genre }}
        </router-link>
      </nav>
    </header>

    <main>
      <router-view />
    </main>
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import movies from './data/movies.js'

const route = useRoute()
const router = useRouter()
const searchText = ref(route.query.q || '')

const genres = computed(() => [...new Set(movies.map((movie) => movie.genre))])

watch(
  () => route.query.q,
  (query) => {
    searchText.value = query || ''
  }
)

function submitSearch() {
  if (!searchText.value) {
    router.push('/')
    return
  }

  router.push({ name: 'search', query: { q: searchText.value } })
}
</script>
