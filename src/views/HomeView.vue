<template>
  <section class="hero">
    <div class="hero-copy">
      <p class="eyebrow">Now showing</p>
      <h1>Find your next movie night pick.</h1>
      <p>
        Browse fantasy, animation, adventure, and sci-fi favorites in one bright,
        simple movie website.
      </p>
    </div>
  </section>

  <section class="content-section">
    <div class="section-heading">
      <div>
        <p class="eyebrow">Collection</p>
        <h2>All Movies Here</h2>
      </div>
      <span>{{ movies.length }} movies</span>
    </div>

    <div class="movie-grid">
      <MovieCard
        v-for="movie in movies"
        :key="movie.id"
        :movie="movie"
        @click="$router.push(`/movies/${movie.id}`)"
      />
    </div>
  </section>
</template>

<script setup>
import MovieCard from '../components/MovieCard.vue'
import movies from '../data/movies.js'
</script>
