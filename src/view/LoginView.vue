<template>
  <div class="full-screen-container">
    <div class="login-card">
      <h2>Login</h2>
      <form @submit.prevent="onSubmit">
        <div class="form-group">
          <label for="email">Email</label>
          <input
            v-model="email"
            type="email"
            id="email"
            required
            placeholder="exemplo@email.com"
          />
        </div>

        <div class="form-group">
          <label for="password">Senha</label>
          <input
            v-model="password"
            type="password"
            id="password"
            required
            placeholder="********"
          />
        </div>

        <button type="submit">Entrar</button>
      </form>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import { users } from '../database/users';

const email = ref<string>('');
const password = ref<string>('');

const emit = defineEmits<{
  (e: 'login', payload: { email: string; password: string }): void;
}>();

function onSubmit() {
  if (!email.value || !password.value) {
    alert('Preencha todos os campos!');
    return;
  }

  const userExists = users.find(
    (user) => user.email === email.value && user.password === password.value
  );

  if (!userExists) {
    alert('Usuário ou senha inválidos!');
    return;
  }

  emit('login', { email: email.value, password: password.value });
}
</script>

<style scoped>
/* ✅ Garantir que o background ocupe toda a tela */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

/* ✅ Container ocupa 100% e centraliza */
.full-screen-container {
  min-height: 100vh;
  min-width: 100vw;
  background: linear-gradient(135deg, #6a0dad, #1e90ff);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Segoe UI', sans-serif;
  box-sizing: border-box;
}

/* ✅ Estilo do cartão de login */
.login-card {
  background: rgba(255, 255, 255, 0.95);
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.25);
  width: 100%;
  max-width: 400px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.login-card h2 {
  text-align: center;
  color: #6a0dad;
  margin-bottom: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  color: #333;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  padding: 0.6rem 1rem;
  border: 2px solid #ccc;
  border-radius: 10px;
  font-size: 1rem;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.form-group input:focus {
  border-color: #6a0dad;
  box-shadow: 0 0 6px #6a0dad88;
  outline: none;
}

button {
  width: 100%;
  padding: 0.75rem;
  background: linear-gradient(to right, #6a0dad, #1e90ff);
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: opacity 0.3s ease-in-out;
}

button:hover {
  opacity: 0.9;
}
</style>
