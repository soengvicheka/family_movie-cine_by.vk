<template>
  <section class="content-section">
    <div class="section-heading">
      <div>
        <p class="eyebrow">Genre</p>
        <h1>{{ genreTitle }}</h1>
      </div>
      <span>{{ filtered.length }} movies</span>
    </div>

    <div class="movie-grid">
      <MovieCard
        v-for="movie in filtered"
        :key="movie.id"
        :movie="movie"
        @click="$router.push(`/movies/${movie.id}`)"
      />
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import MovieCard from '../components/MovieCard.vue'
import movies from '../data/movies.js'

const route = useRoute()
const slug = computed(() => route.params.slug || '')
const genreTitle = computed(() => slug.value.charAt(0).toUpperCase() + slug.value.slice(1))
const filtered = computed(() =>
  movies.filter((movie) => movie.genre.toLowerCase() === slug.value.toLowerCase())
)
</script>
