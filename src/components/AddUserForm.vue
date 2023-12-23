<template>

    <div>
        <h1>Log in</h1>
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
    </div>
</template>

<script setup>

import { ref } from 'vue'
import { useRouter } from 'vue-router'

const firstname = ref('')
const lastname = ref('')
const email = ref('')
const password = ref('')
const role = ref('')
const status = ref('')
const phone = ref('')
const address = ref('')
const router = useRouter()

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
    const response = await fetch('http://localhost:3000/users/', {
        method: 'POST',
        headers: {
        'Content-Type': 'application/json',
        // 'Authorization': 'Bearer ' + localStorage.getItem('token')
        },
        body: JSON.stringify(credentials)
    })

    const data = await response.json()
    console.log(data)
    localStorage.setItem('token', data.token)

    
  router.push('/')
}
</script>