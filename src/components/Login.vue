<template>
    <div>
        <h1>Login</h1>
        <p-inputText v-model="username" placeholder="Username" />
        <p-password v-model="password" placeholder="Password" />
        <p-button label="Login" @click="login" />
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            username: '',
            password: ''
        };
    },
    methods: {
        async login() {
            try {
                const response = await axios.post('/api/login', {
                    username: this.username,
                    password: this.password
                });
                // Handle login success (store token, redirect to dashboard)
            } catch (error) {
                console.error('Login failed:', error);
            }
        }
    }
};
</script>
