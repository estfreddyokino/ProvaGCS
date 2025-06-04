<template>
  <div class="container">
    <nav class="navbar">
      <div class="nav-left">
        <button @click="navigate('home')">Home</button>
        <button @click="navigate('alunos')">Alunos</button>

      </div>
      <div class="nav-right">
        <button @click="showModal = true">Sair</button>
      </div>
    </nav>

    <main class="content">
      <h1>Bem-vindo, {{ userEmail }}!</h1>

      <div v-if="currentPage === 'home'">
        <p>Esta é a página inicial.</p>
      </div>

      <div v-if="currentPage === 'alunos'">
        <AlunosView />
      </div>
    </main>

    <div v-if="showModal" class="modal-overlay">
      <div class="modal">
        <p>Quer realmente sair?</p>
        <div class="modal-buttons">
          <button class="btn-sim" @click="logout">Sim</button>
          <button class="btn-nao" @click="showModal = false">Não</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import AlunosView from './AlunosView.vue';

const props = defineProps<{ userEmail: string }>();
const emit = defineEmits<{ (e: 'logout'): void }>();

const currentPage = ref('home');
const showModal = ref(false);

function navigate(page: string) {
  currentPage.value = page;
}

function logout() {
  emit('logout');
}
</script>

<style scoped>
.container {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.navbar {
  display: flex;
  gap: 1rem;
  background: #6a0dad;
  padding: 1rem;
}

.navbar button {
  color: white;
  background: transparent;
  border: none;
  cursor: pointer;
  font-weight: bold;
}

.content {
  flex: 1;
  padding: 2rem;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: white;
  padding: 2rem;
  border-radius: 10px;
}


.modal-buttons {
  display: flex;
  gap: 1rem;
}

.btn-sim {
  background-color: #28a745;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  cursor: pointer;
}

.btn-nao {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  cursor: pointer;
}
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background: linear-gradient(to right, #6a0dad, #1e90ff);
  color: white;
  font-family: 'Segoe UI', sans-serif;
}

.nav-left, .nav-right {
  display: flex;
  gap: 1rem;
}

.nav-left a {
  color: white;
  text-decoration: none;
  font-weight: bold;
  transition: opacity 0.3s;
}

.nav-left a:hover {
  opacity: 0.8;
}

.nav-right button {
  background: none;
  border: 1px solid white;
  padding: 0.4rem 0.8rem;
  border-radius: 6px;
  color: white;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.3s, opacity 0.3s;
}

.nav-right button:hover {
  background: rgba(255, 255, 255, 0.2);
}
</style>