<template>
  <div class="card"></div>
</template>

<script setup lang="ts"></script>

<style scoped>
.card {
  width: var(--card-width);
  height: var(--card-height);
  background-image: url('src/assets/closed-card.svg');
  background-repeat: no-repeat;
  background-size: cover;
  opacity: 0.3;
  position: relative;
  box-sizing: border-box;
  border: var(--card-border-size) solid #fff;
  border-radius: var(--card-border-radius);
}
</style>
