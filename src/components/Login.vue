<script setup>
import { useForm, useField } from 'vee-validate'
import { loginSchema as validationSchema } from '@/validation/loginSchema'
import { useAuthStore } from '@/stores/auth'

const { handleSubmit } = useForm({ validationSchema })
const auth = useAuthStore()

const email = useField('email')
const password = useField('password')

const submit = handleSubmit((values) => {
  auth.login(values)
  console.log(values)
})
</script>

<template>
  <div class="flex h-screen justify-center items-center">
    <div class="max-w-md w-full space-y-8 shadow-[0px_0px_15px_5px_rgba(0,0,0,0.17)] p-4 rounded-md">
      <div class="text-center">
        <h2 class="text-3xl font-bold text-gray-900">Login</h2>
        <p class="text-sm text-gray-600">Enter your email and password to login</p>
      </div>
      <form @submit="submit" class="space-y-6">
        <div>
          <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
          <input
            type="email"
            id="email"
            v-model="email.value.value"
            name="email"
            class="block w-full rounded-md border-0 py-1.5 px-3 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600"
          />
          <span v-if="email.errorMessage" class="text-sm text-red-600 mt-1 block">{{ email.errorMessage }}</span>
        </div>
        <div>
          <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
          <input
            type="password"
            id="password"
            v-model="password.value.value"
            name="password"
            class="block w-full rounded-md border-0 py-1.5 px-3 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600"
          />
          <span v-if="password.errorMessage" class="text-sm text-red-600 mt-1 block">{{ password.errorMessage }}</span>
        </div>
        <div class="flex items-center justify-between">
          <button type="submit" class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
            Login
          </button>
          <a href="#" class="text-sm text-gray-600 hover:text-gray-900">Forgot password?</a>
        </div>
      </form>
    </div>
  </div>
</template>
