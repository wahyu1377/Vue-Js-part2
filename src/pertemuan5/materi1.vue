<script setup>  
import { ref } from 'vue';  

const items = ref([  
  { id: 1, name: 'Item 1' },  
  { id: 2, name: 'Item 2' },  
  { id: 3, name: 'Item 3' }  
]);  

const newItem = ref('');  

const addItem = () => {  
  if (newItem.value.trim() === '') return;  
  items.value.push({ id: items.value.length + 1, name: newItem.value });  
  newItem.value = '';  
};  

const removeItem = (id) => {  
  items.value = items.value.filter(item => item.id !== id);  
};  
</script>  

<template>  
  <div>  
    <h2>Belajar v-for dengan ref</h2>  
    <input v-model="newItem" placeholder="Tambah item baru">  
    <button @click="addItem">Tambah</button>  

    <ul>  
      <li v-for="item in items" :key="item.id">  
        {{ item.name }}  
        <button class="delete-btn" @click="removeItem(item.id)">Hapus</button>  
      </li>  
    </ul>  
  </div>  
</template>  
