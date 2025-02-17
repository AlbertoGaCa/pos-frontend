<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <!-- El template permanece igual -->
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white p-8 rounded-lg shadow-md w-96">
      <h1 class="text-2xl font-bold text-center mb-6 text-gray-800">Uniformes Canseco</h1>
      <form @submit.prevent="handleLogin">
        <div class="mb-4">
          <label for="user" class="block text-sm font-medium text-gray-700 mb-1">Select User</label>
          <div class="relative">
            <select
              id="user"
              v-model="selectedUser"
              class="block w-full pl-10 pr-4 py-2 border border-gray-300 rounded-md focus:ring-primary focus:border-primary"
              required
            >
              <option value="" disabled>Choose a user</option>
              <option v-for="user in users" :key="user.id" :value="user.id">
                {{ user.name }}
              </option>
            </select>
            <span class="absolute left-3 top-2.5 text-gray-400">
              <UserIcon class="w-5 h-5" />
            </span>
          </div>
        </div>
        <div class="mb-6">
          <label for="password" class="block text-sm font-medium text-gray-700 mb-1"
            >Password</label
          >
          <div class="relative">
            <input
              id="password"
              v-model="password"
              type="password"
              class="block w-full pl-10 pr-4 py-2 border border-gray-300 rounded-md focus:ring-primary focus:border-primary"
              required
            />
            <span class="absolute left-3 top-2.5 text-gray-400">
              <Lock class="w-5 h-5" />
            </span>
          </div>
          <p v-if="errorMessage" class="mt-2 text-sm text-red-600">{{ errorMessage }}</p>
        </div>
        <button
          type="submit"
          class="w-full bg-primary text-white py-2 px-4 rounded-md hover:bg-primary-dark transition duration-300"
        >
          Log In
        </button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { User as UserIcon, Lock } from 'lucide-vue-next'

interface User {
  id: number
  name: string
}

const users: User[] = [
  { id: 1, name: 'Cashier 1' },
  { id: 2, name: 'Cashier 2' },
  { id: 3, name: 'Manager' },
]

const selectedUser = ref<number | string>('')
const password = ref('')
const errorMessage = ref('')

const handleLogin = () => {
  // Validación de tipo para el usuario seleccionado
  if (typeof selectedUser.value !== 'number') {
    errorMessage.value = 'Please select a valid user'
    return
  }

  // Simulación de validación de contraseña
  if (password.value === 'correct123') {
    errorMessage.value = ''
    alert('Login successful!')
    // Redirección lógica aquí
  } else {
    errorMessage.value = 'Incorrect password. Please try again.'
    password.value = ''
  }
}
</script>

<style>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';

:root {
  --color-primary: #4f46e5;
  --color-primary-dark: #4338ca;
}

.bg-primary {
  background-color: var(--color-primary);
}

.hover\:bg-primary-dark:hover {
  background-color: var(--color-primary-dark);
}

.focus\:ring-primary:focus {
  --tw-ring-color: var(--color-primary);
}

.focus\:border-primary:focus {
  border-color: var(--color-primary);
}
</style>
