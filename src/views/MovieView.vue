<template>
  <section v-if="movie" class="movie-detail">
    <div class="watch-preview">
      <img :src="movie.poster" :alt="movie.title" />
      <a class="play-button" :href="watchUrl" target="_blank" rel="noreferrer">
        Watch now
      </a>
    </div>

    <div class="detail-copy">
      <router-link class="back-link" to="/">Back to movies</router-link>
      <p class="eyebrow">{{ movie.genre }}</p>
      <h1>{{ movie.title }}</h1>
      <p>{{ movie.description }}</p>

      <div class="detail-actions">
        <a class="primary-link" :href="watchUrl" target="_blank" rel="noreferrer">
          Watch now
        </a>

        <router-link class="secondary-link" :to="`/genre/${movie.genre}`">
          More {{ movie.genre }} movies
        </router-link>
      </div>
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
const watchUrl = computed(() => {
  if (!movie.value) {
    return '#'
  }

  if (movie.value.watchUrl) {
    return movie.value.watchUrl
  }

  return `https://www.youtube.com/results?search_query=${encodeURIComponent(
    `${movie.value.title} official movie trailer`
  )}`
})
</script>
