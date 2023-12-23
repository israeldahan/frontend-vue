<template>
    <main>
        <AddUserForm />
    </main>
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
import AddUserForm from '@/components/AddUserForm.vue'
const users = ref([])

const fetchUsers = async () => {
    const response = await fetch('http://localhost:3000/users')
    users.value = await response.json()
}

fetchUsers()

</script>