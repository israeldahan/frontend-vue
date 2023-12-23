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
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const router = useRouter()

const login = async () => {
  const credentials = {
    email: email.value,
    password: password.value
  }
    const response = await fetch('http://localhost:3000/users/login', {
        method: 'POST',
        headers: {
        'Content-Type': 'application/json'
        },
        body: JSON.stringify(credentials)
    })

    const data = await response.json()
    console.log(data)
    localStorage.setItem('token', data.token)

    
  router.push('/')
}

</script>

<style scoped>

</style>
