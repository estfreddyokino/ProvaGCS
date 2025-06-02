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
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

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

.login-card {
  background: rgba(255, 255, 255, 0.95);
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.25);
  width: 100%;
  max-width: 360px;
  display: flex;
  flex-direction: column;
}

.login-card h2 {
  text-align: center;
  color: #6a0dad;
  margin-bottom: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem; 
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.25rem; 
}

.form-group label {
  color: #333;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  max-width: 95%; 
  padding: 0.5rem 0.75rem;
  border: 1.5px solid #ccc;
  border-radius: 8px;
  font-size: 0.95rem;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.form-group input:focus {
  border-color: #6a0dad;
  box-shadow: 0 0 5px #6a0dad88;
  outline: none;
}

button {
  width: 100%;
  max-width: 300px; 
  padding: 0.6rem; 
  background: linear-gradient(to right, #6a0dad, #1e90ff);
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: bold;
  cursor: pointer;
  transition: opacity 0.3s ease-in-out;
  align-self: center; 
  margin-top: 0.5rem; 
}

button:hover {
  opacity: 0.9;
}
</style>