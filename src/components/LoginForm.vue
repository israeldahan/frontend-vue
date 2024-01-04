<template>

    <div>
        <h1>Log in</h1>
        <form @submit.prevent="login">
            <div>
            <label for="email">Email</label>
            <input type="email" id="email" v-model="email" />
            </div>
            <div>
            <label for="password">Password</label>
            <input type="password" id="password" v-model="password" />
            </div>
            <button type="submit">Log in</button>
        </form>
    </div>
</template>
  
<script setup>

import { ref } from 'vue'

const email = ref('')
const password = ref('')

const login = async () => {
  const credentials = {
    email: email.value,
    password: password.value
  }
    const response = await fetch(`https://${import.meta.env.VITE_HOST_API}/users/login`, {
        method: 'POST',
        headers: {
        'Content-Type': 'application/json'
        },
        body: JSON.stringify(credentials)
    })

    const data = await response.json()
    console.log(data)
    localStorage.setItem('token', data.token)

    
}

</script>

<style scoped>

</style>
