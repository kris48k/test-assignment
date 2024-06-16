<template>
  <div class="open-card" :class="`open-card--${props.card.suit}`">
    <div class="open-card__rank">{{ props.card.rank }}</div>
    <div class="open-card__suit">
      <Suit :suit="props.card.suit" />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { ICard } from '@/types/ICard'
import Suit from './Suit.vue'

const props = defineProps<{
  card: ICard
}>()
</script>

<style lang="scss" scoped>
.open-card {
  width: 100%;
  height: 100%;
  background-color: #ffffff;
  border-radius: var(--card-border-radius);
  position: relative;

  &--hearts,
  &--diamonds {
    color: red;
  }

  &__rank {
    font-weight: 600;
    font-size: 2em;
    // line-height: 57.61px;
    font-family: 'bahnschriftregular', arial, sans-serif;
    position: absolute;
    top: 0.2em;
    left: 0.5em;
  }

  &__suit {
    position: absolute;
    top: 3em;
    left: 1.5em;
  }
}
</style>
