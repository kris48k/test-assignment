<template>
  <div class="game">
    <div class="game__pile">
      <OpenCard :card="{ rank: 'Q', suit: 'hearts' }" />
    </div>

    <TransitionGroup
      name="flipping-card"
      :duration="{ enter: 5000, leave: 5000 }"
      class="game__cards-to-choose"
      tag="div"
    >
      <FlippingCard
        v-for="card in cards"
        :card="card"
        @afterFlip="onFlipFinished"
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

const middleCardFlipped = ref<boolean>(false)
const cards = ref<ICard[]>([
  { rank: 'Q', suit: 'spades' },
  { rank: 'J', suit: 'hearts' },
  { rank: '5', suit: 'clubs' }
])

function onFlipBtnClick() {
  cards.value.splice(1, 1)
  middleCardFlipped.value = true
}

function onFlipFinished() {}
</script>

<style lang="scss">
.game {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100svh;
  row-gap: 50px;
  overflow: auto;

  &__pile {
    width: clamp(120px, 20vw, 185px);
    height: clamp(180px, 30vw, 276px);
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
  }
}

.flipping-card-enter-active,
.flipping-card-leave-active {
  transition: all 5s ease;
  border: red 1px solid;
}

.flipping-card-leave-active {
  .card__side--back {
    animation: flip-back 3s ease-in;
  }
  .card__side--front {
    animation: flip-front 3s ease-in;
  }
}
</style>
