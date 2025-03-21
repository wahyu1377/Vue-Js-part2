<script setup>
import { ref, watch } from 'vue';


const name = ref('');


watch(name, (newValue, oldValue) => {
  console.log(`Nama berubah dari "${oldValue}" menjadi "${newValue}"`);
  if (newValue.toLowerCase() === 'vue') {
    alert('Ketik "Vue"!');
  }
});
</script>

<template>
  <div class="container">
    <h1>Belajar Watchers di Vue.js</h1>
    <input v-model="name" placeholder="Ketik sesuatu..." />
    <p>Hasil Input: {{ name }}</p>
  </div>
</template>

<style scoped>
input {
  width: 100%;
  padding: 8px;
  margin: 10px 0;
  border-radius: 5px;
  border: 1px solid #ccc;
}
</style>
