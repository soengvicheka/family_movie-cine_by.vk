<template>
  <article class="movie-card" @click="$emit('click')">
    <div class="poster-wrap">
      <img :src="movie.poster" :alt="movie.title" class="poster" />
      <span class="badge">{{ movie.genre }}</span>
    </div>

    <div class="info">
      <h3>{{ movie.title }}</h3>
      <p>{{ movie.description }}</p>
      <button class="card-action" type="button">View movie</button>
    </div>
  </article>
</template>

<script setup>
defineProps({
  movie: {
    type: Object,
    required: true
  }
})

defineEmits(['click'])
</script>
