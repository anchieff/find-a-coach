<template>
    <header class="container mx-auto">
        <nav class="flex justify-between items-center py-4 px-6">
            <h1 class="text-xl font-medium text-purple-900">
                <router-link to="/">Find a Coach</router-link>
            </h1>
            <ul class="list-none flex items-center">
                <li class="pr-4">
                    <router-link to="/coaches">All Coaches</router-link>
                </li>
                <li v-if="isLoggedIn">
                    <router-link to="/requests">Requests</router-link>
                </li>
                <li v-else>
                    <router-link to="/auth">Login</router-link>
                </li>
                <li v-if="isLoggedIn">
                    <base-button class="ml-4" mode="flat" @click="logout"
                        >Logout</base-button
                    >
                </li>
            </ul>
        </nav>
    </header>
</template>

<script>
import BaseButton from '../ui/BaseButton.vue'
export default {
    components: { BaseButton },
    computed: {
        isLoggedIn() {
            return this.$store.getters.isAuthenticated
        },
    },
    methods: {
        logout() {
            this.$store.dispatch('logout')
            this.$router.replace('/coaches')
        },
    },
}
</script>
