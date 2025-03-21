<script setup>
import { ref, computed } from 'vue';

const hargaAsli = ref(100000);
const diskon = ref(10);

const hargaSetelahDiskon = computed(() => {
  return hargaAsli.value - (hargaAsli.value * diskon.value) / 100;
});
</script>

<template>
  <div class="container">
    <h1>Hitung Diskon Harga Produk</h1>
    <label>Harga Asli (Rp):</label>
    <input type="number" v-model="hargaAsli" />

    <label>Persentase Diskon (%):</label>
    <input type="number" v-model="diskon" />

    <h2>Harga Setelah Diskon: Rp {{ hargaSetelahDiskon.toLocaleString('id-ID') }}</h2>
  </div>
</template>

<style scoped>

input {
  display: block;
  width: 100%;
  padding: 8px;
  margin: 10px 0;
  border-radius: 5px;
  border: 1px solid #0da00f;
}
</style>
