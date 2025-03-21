<script setup>
import { ref } from 'vue';

// Variabel reaktif untuk menyimpan teks input
const text = ref('');
</script>

<template>
  <div>
    <h2>Ketikan Sesuatu</h2>
    <input v-model="text" placeholder="Ketik sesuatu di sini...">
    <p>Hasil: <span>{{ text }}</span></p>
  </div>
</template>