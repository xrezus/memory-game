<template>
  <div class="container">
    <GameInfo
        :moves="moves"
        :matched-pairs="matchedPairs"
        :total-pairs="totalPairs"
        :formatted-time="formattedTime"
    />

    <CardGrid
        :cards="cards"
        @flip-card="flipCard"
    />

    <GameControls
        :game-started="gameStarted"
        @start="startGame"
        @reset="resetGame"
    />

    <WinModal
        :show="gameWon"
        :moves="moves"
        :formatted-time="formattedTime"
        @play-again="resetGame"
    />
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from "vue";
import GameInfo from "@/components/GameInfo.vue";
import CardGrid from "@/components/CardGrid.vue";
import GameControls from "@/components/GameControls.vue";
import WinModal from "@/components/WinModal.vue";

// Состояние игры
const cards = ref([]);
const flippedCards = ref([]);
const moves = ref(0);
const matchedPairs = ref(0);
const gameStarted = ref(false);
const gameWon = ref(false);
const timer = ref(0);
const timerInterval = ref(null);

// Настройки игры
const cardValues = ['🍎', '🍌', '🍒', '🍇', '🍊', '🍓', '🍉', '🥭'];
const totalPairs = computed(() => cardValues.length);

// Отформатированное время
const formattedTime = computed(() => {
  const minutes = Math.floor(timer.value / 60);
  const seconds = timer.value % 60;
  return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
});

// Инициализация карточек
const initializeCards = () => {
  let cardDeck = [];

  // Создаем пары карточек
  cardValues.forEach(value => {
    cardDeck.push({value, isFlipped: false, isMatched: false});
    cardDeck.push({value, isFlipped: false, isMatched: false});
  });

  // Перемешиваем карточки
  cardDeck = cardDeck.sort(() => Math.random() - 0.5);
  cards.value = cardDeck;
};

// Начать игру
const startGame = () => {
  gameStarted.value = true;
  startTimer();
};

// Запустить таймер
const startTimer = () => {
  if (timerInterval.value) clearInterval(timerInterval.value);
  timer.value = 0;
  timerInterval.value = setInterval(() => {
    timer.value++;
  }, 1000);
};

// Перевернуть карточку
const flipCard = (card) => {
  if (!gameStarted.value || gameWon.value) return;
  if (card.isFlipped || card.isMatched) return;
  if (flippedCards.value.length >= 2) return;

  card.isFlipped = true;
  flippedCards.value.push(card);

  if (flippedCards.value.length === 2) {
    moves.value++;
    checkForMatch();
  }
};

// Проверить совпадение
const checkForMatch = () => {
  const [card1, card2] = flippedCards.value;

  if (card1.value === card2.value) {
    // Совпадение найдено
    setTimeout(() => {
      card1.isMatched = true;
      card2.isMatched = true;
      flippedCards.value = [];
      matchedPairs.value++;

      // Проверка на победу
      if (matchedPairs.value === totalPairs.value) {
        gameWon.value = true;
        clearInterval(timerInterval.value);
      }
    }, 500);
  } else {
    // Карточки не совпадают
    setTimeout(() => {
      card1.isFlipped = false;
      card2.isFlipped = false;
      flippedCards.value = [];
    }, 1000);
  }
};

// Сбросить игру
const resetGame = () => {
  clearInterval(timerInterval.value);
  moves.value = 0;
  matchedPairs.value = 0;
  flippedCards.value = [];
  gameStarted.value = false;
  gameWon.value = false;
  timer.value = 0;
  initializeCards();
};

// Инициализация при загрузке
onMounted(() => {
  initializeCards();
});
</script>

<style scoped>
.container {
  width: 1240px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  padding: 30px;
  text-align: center;
}
</style>