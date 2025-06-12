<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-100 to-white flex items-center justify-center px-4">
    <div class="bg-white shadow-lg rounded-2xl p-8 max-w-lg w-full space-y-6">
      <h1 class="text-3xl font-bold text-center text-blue-700">Webhook Tester</h1>
      <p class="text-gray-600 text-center">Test your webhook endpoint using your email and endpoint URL</p>

      <form @submit.prevent="handleSubmit" class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Email address</label>
          <input
            v-model="email"
            type="email"
            required
            placeholder="your@email.com"
            class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">API Endpoint URL</label>
          <input
            v-model="url"
            type="url"
            required
            placeholder="https://your-api.vercel.app"
            class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400"
          />
        </div>

        <button
          type="submit"
          class="w-full bg-blue-600 text-white font-semibold py-3 rounded-lg hover:bg-blue-700 transition"
        >
          Test Webhook
        </button>
      </form>

      <div v-if="response" class="bg-gray-50 border border-gray-200 rounded-lg p-4 text-sm font-mono whitespace-pre-wrap">
        {{ response }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
const url = ref('')
const response = ref(null)

const handleSubmit = async () => {
  response.value = '⏳ Testing...'

  const testUrl = `https://yhxzjyykdsfkdrmdxgho.supabase.co/functions/v1/junior-dev?url=${encodeURIComponent(
    url.value
  )}&email=${encodeURIComponent(email.value)}`

  try {
    const res = await fetch(testUrl)
    const result = await res.json()
    response.value = JSON.stringify(result, null, 2)
  } catch (err) {
    response.value = '❌ Error: ' + err.message
  }
}
</script>
