<template>
  <div class="game-info">
    <div class="info-item">Ходы: <strong>{{ moves }}</strong></div>
    <div class="info-item">Пары: <strong>{{ matchedPairs }}/{{ totalPairs }}</strong></div>
    <div class="info-item">Время: <strong>{{ formattedTime }}</strong></div>
  </div>
</template>

<script setup>
defineProps({
  moves: {
    type: Number,
    required: true
  },
  matchedPairs: {
    type: Number,
    required: true
  },
  totalPairs: {
    type: Number,
    required: true
  },
  formattedTime: {
    type: String,
    required: true
  }
});
</script>

<style scoped>
.game-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 25px;
  background: #f0f8ff;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.info-item {
  font-size: 1.2rem;
  font-weight: 600;
  color: #444;
}

@media (max-width: 600px) {
  .game-info {
    flex-direction: column;
    gap: 10px;
  }
}
</style>


