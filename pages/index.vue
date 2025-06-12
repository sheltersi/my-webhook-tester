<template>
  <div class="p-10 max-w-xl mx-auto space-y-6">
    <h1 class="text-2xl font-bold">Webhook Validator</h1>

    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div>
        <label>Email:</label>
        <input v-model="email" type="email" required class="border p-2 w-full" />
      </div>

      <div>
        <label>API Endpoint URL:</label>
        <input v-model="url" type="url" required class="border p-2 w-full" />
      </div>

      <button type="submit" class="bg-blue-500 text-white px-4 py-2">Test Webhook</button>
    </form>

    <div v-if="response" class="mt-4 p-4 border bg-gray-100">
      <pre>{{ response }}</pre>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
const url = ref('')
const response = ref(null)

const handleSubmit = async () => {
  response.value = 'Testing...'

  const testUrl = `https://yhxzjyykdsfkdrmdxgho.supabase.co/functions/v1/junior-dev?url=${encodeURIComponent(url.value)}&email=${encodeURIComponent(email.value)}`
  try {
    const res = await fetch(testUrl)
    const result = await res.json()
    response.value = result
  } catch (err) {
    response.value = 'Error: ' + err.message
  }
}
</script>
