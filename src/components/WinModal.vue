<template>
  <div class="win-message" v-if="show">
    <div class="win-content">
      <h2>Поздравляем!</h2>
      <p>Вы нашли все пары за {{ moves }} ходов и {{ formattedTime }}!</p>
      <button class="reset-btn" @click="$emit('playAgain')">Играть снова</button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  show: {
    type: Boolean,
    required: true
  },
  moves: {
    type: Number,
    required: true
  },
  formattedTime: {
    type: String,
    required: true
  }
});

defineEmits(['playAgain']);
</script>

<style scoped>
.win-message {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
  animation: fadeIn 0.5s;
}

.win-content {
  background: white;
  padding: 40px;
  border-radius: 20px;
  text-align: center;
  max-width: 500px;
  width: 90%;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.win-content h2 {
  color: #42e695;
  margin-bottom: 20px;
  font-size: 2.5rem;
}

.win-content p {
  font-size: 1.3rem;
  margin-bottom: 25px;
  color: #444;
}

.reset-btn {
  padding: 12px 25px;
  font-size: 1.1rem;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 600;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
  color: white;
}

.reset-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
}

.reset-btn:active {
  transform: translateY(1px);
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>


