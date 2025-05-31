<template>
  <div >
    <h2 >Login</h2>
    <form @submit.prevent="onSubmit">
      <div class="mb-4">
        <label for="email" class="block text-gray-700">Email</label>
        <input
          v-model="email"
          type="email"
          id="email"
          required

        />
      </div>

      <div class="mb-6">
        <label for="password" class="block text-gray-700">Senha</label>
        <input
          v-model="password"
          type="password"
          id="password"
          required
        />
      </div>

      <button
        type="submit"
      >
        Entrar
      </button>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

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
  emit('login', { email: email.value, password: password.value });
}
</script>

<style scoped>

</style>
