<template>
  <div class="game">
    <div class="pile">
      <OpenCard :card="topCard" class="pile__top-card" />
    </div>

    <TransitionGroup
      name="flipping-card"
      :duration="{ enter: 1000, leave: 2000 }"
      class="game__cards-to-choose"
      tag="div"
      @after-leave="onFlipFinished"
    >
      <FlippingCard
        v-for="card in cards"
        :card="card"
        :key="card.rank + card.suit"
        :data-index="card.rank + card.suit"
      />
    </TransitionGroup>

    <button class="game__flip-btn" @click="onFlipBtnClick">Flip middle card</button>
  </div>
</template>

<script setup lang="ts">
import FlippingCard from './FlippingCard.vue'
import OpenCard from './OpenCard.vue'
import { ref } from 'vue'
import type { ICard } from '@/types/ICard'

const cards = ref<ICard[]>([
  { rank: 'J', suit: 'spades' },
  { rank: 'Q', suit: 'hearts' },
  { rank: '10', suit: 'clubs' }
])

const topCard = ref<ICard>({ rank: 'Q', suit: 'spades' })
const movingCard = ref<ICard | null>(null)

function onFlipBtnClick() {
  movingCard.value = cards.value[1]
  cards.value = [cards.value[0], cards.value[2]]
}

function onFlipFinished() {
  if (movingCard.value) {
    topCard.value = movingCard.value
    cards.value.push(movingCard.value)
    movingCard.value = null
  }
}
</script>

<style scoped lang="scss">
.game {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100svh;
  row-gap: var(--lines-gap);
  overflow: auto;
  position: relative;

  .pile {
    width: var(--pile-card-width);
    height: var(--pile-card-height);
    position: relative;

    &__top-card {
      box-shadow:
        0px 4px 0px white,
        0px 4px 4px -2px black,
        0px 8px 0px white,
        0px 8px 4px -2px black,
        0px 12px 0px white,
        0px 12px 4px -2px black,
        0px 16px 0px white,
        0px 16px 4px -2px black;
    }
  }

  &__cards-to-choose {
    display: flex;
    column-gap: 21px;
    justify-content: center;
  }

  &__flip-btn {
    position: absolute;
    right: 10px;
    bottom: 10px;
    width: calc(min(100vw, 345px) - 20px);
    height: 73px;
    border-radius: 12px;
    border: 1px;
    opacity: 0px;
    background: linear-gradient(180deg, #4457ff 0%, #3c4de1 100%);
    border: 1px solid #4456fe;
  }
}
</style>
