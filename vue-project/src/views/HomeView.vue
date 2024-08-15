<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <div>
    <h1>{{ $route.params.name }}</h1>
  </div>
  <RouterLink class="btn btn-primary" to="/">Go back to login page</RouterLink>
</template>


