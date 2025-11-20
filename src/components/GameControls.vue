<template>
  <div class="controls">
    <button class="start-btn" @click="$emit('start')" v-if="!gameStarted">Начать игру</button>
    <button class="reset-btn" @click="$emit('reset')">Новая игра</button>
  </div>
</template>

<script setup>
defineProps({
  gameStarted: {
    type: Boolean,
    required: true
  }
});

defineEmits(['start', 'reset']);
</script>

<style scoped>
.controls {
  display: flex;
  justify-content: center;
  gap: 15px;
}

button {
  padding: 12px 25px;
  font-size: 1.1rem;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 600;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.start-btn {
  background: linear-gradient(135deg, #42e695 0%, #3bb2b8 100%);
  color: white;
}

.reset-btn {
  background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
  color: white;
}

button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
}

button:active {
  transform: translateY(1px);
}
</style>


