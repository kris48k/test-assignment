<template>
  <div class="suit" :class="props.suit">{{ suitSymbol }}</div>
</template>

<script setup lang="ts">
import type { TCardSuits } from '@/types/ICard'
import { computed } from 'vue'

const props = defineProps<{
  suit: TCardSuits
}>()

function getSuitSymbol(suit: TCardSuits): string {
  switch (suit) {
    case 'clubs':
      return '♣'
    case 'diamonds':
      return '♦'
    case 'hearts':
      return '♥'
    case 'spades':
      return '♠'
    default:
      return ''
  }
}

const suitSymbol = computed(() => getSuitSymbol(props.suit))
console.log('kris:', suitSymbol, getSuitSymbol(props.suit))
</script>

<style scoped lang="scss">
.suit {
  font-size: 3em;
}
</style>
