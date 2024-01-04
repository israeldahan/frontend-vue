<template>
    <div>
        <h1>Users</h1>
        <div v-for="user in users" :key="user.id">
            <h2>{{ user.firstName }} {{ user.lastName }}</h2>
            <p>{{ user.email }}</p>
            <p>{{ user.role }}</p>
            <p>{{ user.status }}</p>
            <p>{{ user.phone }}</p>
            <p>{{ user.address }}</p>
        </div>
    </div>
</template>

<script setup>

import { ref } from 'vue'
const users = ref([])

const fetchUsers = async () => {
    const response = await fetch('http://import.meta.env.HOST_API/users', {
        headers: {
            'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
    })
    users.value = await response.json()
}

fetchUsers()

</script>