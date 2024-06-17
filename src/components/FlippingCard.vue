<template>
  <div class="card">
    <ClosedCard class="card__side card__side--back" />
    <OpenCard :card="props.card" class="card__side card__side--front" />
  </div>
</template>

<script setup lang="ts">
import type { ICard } from '@/types/ICard'
import OpenCard from './OpenCard.vue'
import ClosedCard from './ClosedCard.vue'

const props = defineProps<{
  card: ICard
}>()
</script>

<style scoped lang="scss">
.card {
  position: relative;
  -moz-perspective: 200rem;
  perspective: 200rem;
  transform-style: preserve-3d;
  width: var(--card-width);
  height: var(--card-height);
  transition: 1s all ease;
}

.card__side {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.card__side--front {
  transform: rotateY(180deg);
  width: var(--card-width);
  height: var(--card-height);
}

.flipping-card-leave-active {
  .card__side--back {
    animation: flip-back 2s forwards;
  }
  .card__side--front {
    animation: flip-front 2s forwards;
  }
}

.flipping-card-leave-active.card {
  animation: squizing 2s forwards;
}

.flipping-card-enter-active.card {
  animation: showing-up 1s forwards;
}

@keyframes flip-front {
  50% {
    transform: rotateY(0);
    left: 0;
    width: var(--card-width);
    height: var(--card-height);
  }
  100% {
    width: var(--pile-card-width);
    height: var(--pile-card-height);
    left: calc((-1 * var(--pile-card-width) / 2));
    transform: rotateY(0) translateY(calc(-1 * (var(--lines-gap) + var(--pile-card-height))));
  }
}

@keyframes flip-back {
  50% {
    transform: rotateY(-180deg);
  }
  100% {
    transform: rotateY(-180deg) translateY(calc(-1 * (var(--lines-gap) + var(--pile-card-height))));
  }
}

@keyframes squizing {
  50% {
    width: var(--card-width);
  }
  100% {
    width: 0;
  }
}

@keyframes showing-up {
  0% {
    opacity: 0;
    transform: translateX(100px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>
