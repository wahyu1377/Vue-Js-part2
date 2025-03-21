<script setup>
import { ref, computed } from 'vue'
const isDay = ref(true)
const toggleMode = () => {
  isDay.value = !isDay.value
}
const buttonText = computed(() => isDay.value ? "Ubah ke Mode Malam 🌙" : "Ubah ke Mode Siang ☀️")

const message = computed(() => isDay.value ? "Selamat Pagi! 🌞" : "Selamat Malam! 🌙")
</script>

<template>
  <div :class="isDay ? 'day-mode' : 'night-mode'" class="container">
    <button @click="toggleMode">{{ buttonText }}</button>
    <transition name="fade">
      <h1 :key="isDay">{{ message }}</h1>
    </transition>
  </div>
</template>

<style>

.container {
  text-align: center;
  padding: 50px;
  min-height: 50vh;
  transition: background-color 0.5s, color 0.5s;
}

.day-mode {
  background-color: #ffeb3b;
  color: #333;
}

.night-mode {
  background-color: #2c3e50;
  color: white;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

button:hover {
  background-color: #0056b3;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
