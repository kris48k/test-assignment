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
  background-color: white;
  border-radius: var(--card-border-radius);
  box-shadow: 0px 0px 5px gray;

  &--hearts,
  &--diamonds {
    color: red;
  }

  &__rank {
    font-weight: 600;
    font-size: clamp(2em, 6vw, 3.5em);
    font-family: 'bahnschriftregular', arial, sans-serif;
    position: absolute;
    top: 4%;
    left: 15%;
  }

  &__suit {
    position: absolute;
    top: 20%;
    left: 13%;
  }
}
</style>
