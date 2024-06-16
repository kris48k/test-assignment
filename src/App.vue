<script setup lang="ts">
import Game from './components/Game.vue'
</script>

<template>
  <main>
    <Game />
  </main>
</template>

<style scoped>
main {
  background-image: url('assets/bg-desktop.svg');
  background-size: cover;
  background-repeat: no-repeat;
  height: 100vh;
}

@media screen and (max-width: 768px) {
  main {
    background-image: url('assets/bg-mobile.svg');
  }
}
</style>
