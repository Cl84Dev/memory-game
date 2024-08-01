<template>
  <div class="mg-card-container" @click="openCard">
    <div class="mg-card" :class="{ 'mg-open': isFront }">
      <div class="front">
        <img :src="src" alt="" />
      </div>
      <div class="back"></div>
    </div>
  </div>
</template>

<script setup>
import { watch, ref } from "vue";

const emit = defineEmits(["play"]);
const props = defineProps({
  isFront: {
    type: Boolean,
    default: false,
  },
  value: {
    type: String,
  },
});

const src = ref("");

watch(
  () => props.value,
  () => {
    src.value = `../src/assets/characters/${props.value}.png`;
  }
);

const openCard = () => {
  emit("play");
};
</script>

<style>
.mg-card-container {
  perspective: 1000px;
}

.mg-card {
  width: 100px;
  height: 200px;
  position: relative;
  transition: transform 0.5s ease;
  cursor: pointer;
  transform-style: preserve-3d;
}

.front,
.back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 5px;
  user-select: none;
}

.front {
  background-color: var(--mg-primary);
  transform: rotateY(180deg);
  display: flex;
  align-items: center;
  justify-content: center;
}

.back {
  background-color: var(--mg-secondary);
}

.front img {
  width: 75%;
}

.mg-open {
  transform: rotateY(180deg);
}
</style>
