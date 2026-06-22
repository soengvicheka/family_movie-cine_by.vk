<template>
  <section v-if="movie" class="movie-detail">
    <img :src="movie.poster" :alt="movie.title" />

    <div class="detail-copy">
      <router-link class="back-link" to="/">Back to movies</router-link>
      <p class="eyebrow">{{ movie.genre }}</p>
      <h1>{{ movie.title }}</h1>
      <p>{{ movie.description }}</p>

      <router-link class="primary-link" :to="`/genre/${movie.genre}`">
        More {{ movie.genre }} movies
      </router-link>
    </div>
  </section>

  <section v-else class="empty-state">
    <h1>Movie not found</h1>
    <p>This movie is not in the collection.</p>
    <router-link to="/">Back to all movies</router-link>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import movies from '../data/movies.js'

const route = useRoute()
const movie = computed(() => movies.find((item) => item.id === Number(route.params.id)))
</script>
