<template>
  <div class="container">
    <nav class="navbar">
      <button @click="navigate('home')">Home</button>
      <button @click="navigate('alunos')">Alunos</button>
      <button @click="showModal = true">Sair</button>
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
        <button @click="logout">Sim</button>
        <button @click="showModal = false">Não</button>
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
  background: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: white;
  padding: 2rem;
  border-radius: 10px;
}
</style>