<template>
  <div class="page-container">
    <div class="inner-container">
      <div class="btn-start" @click="sortCards">Restart</div>
      <div class="cards-container">
        <Card
          v-for="(card, index) in cards"
          :key="index"
          :is-front="card.isFront"
          :value="card.value"
          @play="play(card.value, index)"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Card from "../components/home/Card.vue";

const cards = ref([
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
  { value: "", isFront: false, isFlipped: false },
]);
const card = ref({ value: "", index: null });
const isLoading = ref(false);

const play = (value, index) => {
  if (
    cards.value[index].isFlipped === true ||
    isLoading.value === true ||
    card.value.index === index
  ) {
    return;
  }

  if (card.value.value !== "") {
    cards.value[index].isFront = true;
    isLoading.value = true;

    if (card.value.value !== value) {
      setTimeout(() => {
        cards.value[card.value.index].isFront = false;
        cards.value[index].isFront = false;
        card.value.index = null;
        card.value.value = "";
        isLoading.value = false;
      }, 500);
    } else {
      cards.value[card.value.index].isFlipped = true;
      cards.value[index].isFlipped = true;
      card.value.index = null;
      card.value.value = "";
      isLoading.value = false;
    }
  } else {
    cards.value[index].isFront = true;
    card.value.index = index;
    card.value.value = value;
  }
};

const sortCards = () => {
  isLoading.value = true;

  const characters = [
    "bowser",
    "daisy",
    "luigi",
    "mario",
    "peach",
    "rosalina",
    "toad",
    "waluigi",
    "wario",
    "yoshi",
    "bowser",
    "daisy",
    "luigi",
    "mario",
    "peach",
    "rosalina",
    "toad",
    "waluigi",
    "wario",
    "yoshi",
  ];

  const listControl = [];

  characters.forEach((item) => {
    const randomNumber = Math.floor(Math.random() * 2);
    if (randomNumber === 0) {
      listControl.push(item);
    } else {
      listControl.unshift(item);
    }
  });

  cards.value.forEach((item) => (item.isFront = false));
  card.value.index = null;
  card.value.value = "";

  setTimeout(() => {
    listControl.forEach((item, index) => {
      cards.value[index].isFlipped = false;
      cards.value[index].value = item;
    });

    isLoading.value = false;
  }, 500);
};

onMounted(() => {
  sortCards();
});
</script>

<style>
.cards-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  place-content: center;
  gap: 4px;
  width: 70%;
}

.inner-container {
  min-height: 100vh;
  min-width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 32px;
}

.btn-start {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 120px;
  height: 35px;
  background-color: var(--mg-primary);
  color: var(--mg-white);
  font-weight: bold;
  font-size: 1.3rem;
  border-radius: 5px;
  cursor: pointer;
  user-select: none;
}

.btn-start:active {
  border: 1px solid var(--mg-silver);
  color: var(--mg-silver);
}
</style>
