<template>
  <div>
    <h2>Alunos</h2>

    <form @submit.prevent="addAluno">
      <input v-model="novoAluno" placeholder="Nome do aluno" required />
      <button type="submit">Adicionar</button>
    </form>

    <ul>
      <li v-for="(aluno, index) in alunos" :key="index">
        {{ aluno }}
        <button @click="removerAluno(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, watch } from 'vue';

const alunos = ref<string[]>([]);
const novoAluno = ref<string>('');


onMounted(() => {
  const dados = localStorage.getItem('alunos');
  if (dados) {
    alunos.value = JSON.parse(dados);
  }
});


watch(alunos, (novoValor) => {
  localStorage.setItem('alunos', JSON.stringify(novoValor));
}, { deep: true });

function addAluno() {
  if (novoAluno.value.trim() !== '') {
    alunos.value.push(novoAluno.value.trim());
    novoAluno.value = '';
  }
}

function removerAluno(index: number) {
  alunos.value.splice(index, 1);
}
</script>

<style scoped>
form {
  margin-bottom: 1rem;
}

input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 0.5rem;
}

button {
  padding: 0.5rem 1rem;
  background: #6a0dad;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 0.5rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>