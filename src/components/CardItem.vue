<script setup>
defineProps({
  card: {
    type: Object,
    required: true
  },
  index: {
    type: Number,
    required: true
  }
});

defineEmits(['flip']);
</script>

<template>
  <div
      class="card"
      :class="{ flipped: card.isFlipped, matched: card.isMatched }"
      @click="$emit('flip')"
  >
    <div class="card-front">
      <span v-if="card.isFlipped">{{ card.value }}</span>
    </div>
    <div class="card-back"></div>
  </div>
</template>

<style scoped>
.card {
  aspect-ratio: 3/2;
  background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transform-style: preserve-3d;
  transition: transform 0.5s;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  font-size: 6.5rem;
  user-select: none;
}

.card.flipped {
  transform: rotateY(180deg);
}

.card.matched {
  visibility: hidden;
}

.card-front, .card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card-front {
  background: white;
  transform: rotateY(180deg);
}

.card-back {
  background: url('/tiki.png');
  color: white;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 30px 0px;
}
</style>