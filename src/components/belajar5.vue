<script setup>
import { ref, computed, watch } from 'vue';

let id = 0;
const newTodo = ref('');
const hideCompleted = ref(false);
const todos = ref(JSON.parse(localStorage.getItem('todos')) || [
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
]);
const editTodoId = ref(null);
const editTodoText = ref('');
const sortBy = ref('default');

watch(todos, (newTodos) => {
  localStorage.setItem('todos', JSON.stringify(newTodos));
}, { deep: true });

const filteredTodos = computed(() => {
  let list = hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
  if (sortBy.value === 'name') {
    return [...list].sort((a, b) => a.text.localeCompare(b.text));
  } else if (sortBy.value === 'status') {
    return [...list].sort((a, b) => a.done - b.done);
  }
  return list;
});

function addTodo() {
  if (newTodo.value.trim() === '') return;
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = '';
}

function startEdit(todo) {
  editTodoId.value = todo.id;
  editTodoText.value = todo.text;
}

function saveEdit(todo) {
  todo.text = editTodoText.value;
  editTodoId.value = null;
}
function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}

function removeCompleted() {
  todos.value = todos.value.filter((t) => !t.done);
}
</script>

<template>
  <div class="container">
    <h1>📌 To-Do List</h1>

    <form @submit.prevent="addTodo" class="form">
      <input v-model="newTodo" placeholder="Tambah tugas..." required />
      <button>➕ Tambah</button>
    </form>

    <div class="options">
      <select v-model="sortBy">
        <option value="default">Urutan Default</option>
        <option value="name">Urutkan Berdasarkan Nama</option>
        <option value="status">Urutkan Berdasarkan Status</option>
      </select>
      <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted ? 'Tampilkan Semua' : 'Sembunyikan Selesai' }}
      </button>
    </div>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.done">
        <span v-if="editTodoId !== todo.id" @dblclick="startEdit(todo)">
          {{ todo.text }} - <strong>{{ todo.done ? '✅' : '❌' }}</strong>
        </span>
        <input v-else v-model="editTodoText" @keyup.enter="saveEdit(todo)" @blur="saveEdit(todo)">
        <button class="delete-btn" @click="removeTodo(todo)">❌</button>
      </li>
    </ul>

    <button @click="removeCompleted" v-if="todos.some(t => t.done)">🗑 Hapus Selesai</button>
  </div>
</template>

<style scoped>
.container {
  max-width: 400px;
  margin: auto;
  background: #201d1da2;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}
.form {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}
.options {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}
input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
button {
  background: #3498db;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;
}
button:hover {
  background: #2980b9;
}
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px;
  border-bottom: 1px solid #eee;
}
.todo-item input[type="text"] {
  flex: 1;
  border: 1px solid #ccc;
  padding: 4px;
  border-radius: 5px;
}
.delete-btn {
  background:rgb(23, 176, 66);
  padding: 4px 8px;
}
.delete-btn:hover {
  background: #c0392b;
}
</style>
