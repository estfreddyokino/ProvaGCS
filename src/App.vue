<template>
  <LoginView @login="handleLogin" />
</template>

<script lang="ts" setup>
import LoginView from './view/LoginView.vue';

function handleLogin(payload: { email: string; password: string }) {
  console.log('Login realizado:', payload);
}
</script>