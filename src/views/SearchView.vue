<template>
  <section class="content-section">
    <div class="section-heading">
      <div>
        <p class="eyebrow">Search</p>
        <h1>{{ title }}</h1>
      </div>
      <span>{{ results.length }} found</span>
    </div>

    <div v-if="results.length" class="movie-grid">
      <MovieCard
        v-for="movie in results"
        :key="movie.id"
        :movie="movie"
        @click="$router.push(`/movies/${movie.id}`)"
      />
    </div>

    <div v-else class="empty-state">
      <h2>No movies found</h2>
      <p>Try searching another title or genre.</p>
      <router-link to="/">Back to all movies</router-link>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import MovieCard from '../components/MovieCard.vue'
import movies from '../data/movies.js'

const route = useRoute()

const query = computed(() => (route.query.q || '').toString().trim().toLowerCase())
const title = computed(() => (query.value ? `Results for "${route.query.q}"` : 'Search movies'))

const results = computed(() => {
  if (!query.value) {
    return movies
  }

  return movies.filter((movie) => {
    const searchableText = `${movie.title} ${movie.genre} ${movie.description}`.toLowerCase()
    return searchableText.includes(query.value)
  })
})
</script>
