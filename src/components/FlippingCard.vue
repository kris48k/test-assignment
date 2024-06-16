<template>
  <!-- <Transition name="flipping-card" :duration="{ enter: 50000, leave: 1000 }" class="card"> -->
  <div class="card">
    <ClosedCard class="card__side card__side--back" />
    <OpenCard :card="props.card" class="card__side card__side--front" />
  </div>
  <!-- </Transition> -->
</template>

<script setup lang="ts">
import type { ICard } from '@/types/ICard'
import OpenCard from './OpenCard.vue'
import ClosedCard from './ClosedCard.vue'

const props = defineProps<{
  card: ICard
}>()
</script>

<style lang="scss">
.card {
  position: relative;
  -moz-perspective: 200rem;
  perspective: 200rem;
  transform-style: preserve-3d;
  width: var(--card-width);
  height: var(--card-height);
}

.card__side {
  height: 100%;
  transition: all 1s ease;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.card__side--front {
  transform: rotateY(180deg);
  width: var(--card-width);
  height: var(--card-height);
}

:deep(.flipping-card-leave-active) {
  .card__side--back {
    animation: flip-back 3s ease-in;
  }
  .card__side--front {
    animation: flip-front 3s ease-in;
  }
}

@keyframes flip-front {
  25% {
    transform: rotateY(0);
  }
  35% {
    transform: translateY(-240px);
  }
}

@keyframes flip-back {
  25% {
    transform: rotateY(-180deg);
  }
}
</style>
