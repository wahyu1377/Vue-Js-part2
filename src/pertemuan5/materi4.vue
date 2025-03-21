<script setup>
import { ref, onMounted } from 'vue';


const inputRef = ref(null);
const boxRef = ref(null);


onMounted(() => {
  if (inputRef.value) {
    inputRef.value.focus(); 
  }
  if (boxRef.value) {
    boxRef.value.style.backgroundColor = 'lightblue';
  }
});


const changeColor = () => {
  boxRef.value.style.backgroundColor =
    boxRef.value.style.backgroundColor === 'lightblue' ? 'lightcoral' : 'lightblue';
};
</script>

<template>
  <div class="container">
    <h1>Belajar Template Refs & Lifecycle Hook</h1>

    <!-- Input dengan ref -->
    <input ref="inputRef" placeholder="Input ini auto-focus" />
    <div ref="boxRef" class="box">
      berubah warna 
    </div>
    <button @click="changeColor">Ubah warna</button>
  </div>
</template>

<style scoped>
.container {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  text-align: center;
}
input {
  width: 100%;
  padding: 8px;
  margin: 10px 0;
  border-radius: 5px;
  border: 1px solid #ccc;
}
.box {
  width: 100%;
  height: 100px;
  margin: 20px 0;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  font-weight: bold;
}
button {
  padding: 10px 15px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
</style>
