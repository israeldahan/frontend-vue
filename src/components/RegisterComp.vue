<template>

    <div>
        <h1>Register</h1>
        <form @submit.prevent="login">
            <div>
            <label for="firstname">First Name</label>
            <input type="firstname" id="firstname" v-model="firstname" />
            </div>
            <div>
            <label for="lastname">Last Name</label>
            <input type="lastname" id="lastname" v-model="lastname" />
            </div>
            <div>
            <label for="email">Email</label>
            <input type="email" id="email" v-model="email" />
            </div>
            <div>
            <label for="password">Password</label>
            <input type="password" id="password" v-model="password" />
            </div>
            <div>
                <label for="role">Role</label>
                <select id="role" v-model="role">
                    <option value="admin">Admin</option>
                    <option value="user">User</option>
                </select>
            </div>
            <div>
                <label for="status">Status</label>
                <select id="status" v-model="status">
                    <option value="active">Active</option>
                    <option value="inactive">Inactive</option>
                </select>
            </div>
            <div>   
                <label for="address">Address</label>
                <input type="address" id="address" v-model="address" />
            </div>
            <div>   
                <label for="phone">Address</label>
                <input type="phone" id="phone" v-model="phone" />
            </div>
            <button type="submit">Register</button>
        </form>
        <div v-if="result">
            {{ result }}
        </div>
    </div>
</template>

<script setup>

import { ref } from 'vue'

const firstname = ref('')
const lastname = ref('')
const email = ref('')
const password = ref('')
const role = ref('')
const status = ref('')
const phone = ref('')
const address = ref('')
const result = ref('')

const login = async () => {
  const credentials = {
    firstName: firstname.value,
    lastName: lastname.value,
    email: email.value,
    password: password.value,
    role: role.value,
    status: status.value,
    address: address.value,
    phone: phone.value
  }
    const response = await fetch(`http://${import.meta.env.VITE_HOST_API}/users/register`, {
        method: 'POST',
        headers: {
        'Content-Type': 'application/json',
        },
        body: JSON.stringify(credentials)
    })

    const data = await response.json()
    result.value = data
    console.log(data)
    localStorage.setItem('token', data.token)

    
}
</script>