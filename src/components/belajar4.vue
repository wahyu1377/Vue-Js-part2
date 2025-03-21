<script setup>
import { ref } from "vue";

const isLoggedIn = ref(false); 
const isAdmin = ref(false);

const toggleLogin = () => {
  isLoggedIn.value = !isLoggedIn.value;
};

const toggleAdmin = () => {
  if (isLoggedIn.value) {
    isAdmin.value = !isAdmin.value;
  }
};
</script>

<template>
  <div class="container">
    <h1>Conditional Rendering - v-if, v-else-if, v-else</h1>


    <p v-if="isLoggedIn && isAdmin">👑 Selamat datang, Admin!</p>
    <p v-else-if="isLoggedIn">👋 Selamat datang, Pengguna!</p>
    <p v-else>🔒 Silakan login terlebih dahulu.</p>

    <button @click="toggleLogin">
      {{ isLoggedIn ? "Logout" : "Login" }}
    </button>

    <button @click="toggleAdmin" :disabled="!isLoggedIn">
      {{ isAdmin ? "Jadi Pengguna Biasa" : "Jadi Admin" }}
    </button>
  </div>
</template>

<style scoped>
.container {
  text-align: center;
  font-family: Arial, sans-serif;
}

button {
  background: #3498db;
  color: white;
  padding: 8px 12px;
  margin: 5px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

button:disabled {
  background: gray;
  cursor: not-allowed;
}
</style>
