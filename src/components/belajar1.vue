<script setup>
import { ref } from 'vue';

const isRed = ref(true);
</script>

<template>
  <div>
    <button @click="isRed = !isRed">Tekan Ini !!!</button>
    <h1 :style="{ color: isRed ? 'red' : 'blue' }">Belajar Vue</h1>
  </div>
</template>