<template>
  <LoginView v-if="!isLoggedIn" @login="handleLogin" />
  <HomeView v-else :userEmail="user.email" @logout="handleLogout" />
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import LoginView from './view/LoginView.vue';
import HomeView from './view/HomeView.vue';

const isLoggedIn = ref(false);
const user = ref({ email: '', password: '' });

function handleLogin(payload: { email: string; password: string }) {
  user.value = payload;
  isLoggedIn.value = true;
}

function handleLogout() {
  user.value = { email: '', password: '' };
  isLoggedIn.value = false;
}
</script>
<style>
html, body, #app {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}
</style>