<template>
  <article
    class="movie-card"
    role="button"
    tabindex="0"
    @click="$emit('click')"
    @keydown.enter="$emit('click')"
    @keydown.space.prevent="$emit('click')"
  >
    <div class="poster-wrap">
      <img :src="movie.poster" :alt="movie.title" class="poster" />
      <span class="badge">{{ movie.genre }}</span>
    </div>

    <div class="info">
      <h3>{{ movie.title }}</h3>
      <p>{{ movie.description }}</p>
      <button class="card-action" type="button">Watch movie</button>
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
