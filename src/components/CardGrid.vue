<template>
  <div class="cards-grid">
    <CardItem
        v-for="(card, index) in cards"
        :key="index"
        :card="card"
        :index="index"
        @flip="$emit('flipCard', card)"
    />
  </div>
</template>

<script setup>
import CardItem from './CardItem.vue';

defineProps({
  cards: {
    type: Array,
    required: true
  }
});

defineEmits(['flipCard']);
</script>

<style scoped>
.cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
  margin-bottom: 25px;
}

@media (max-width: 600px) {
  .cards-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>


