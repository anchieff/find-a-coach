<template>
    <header class="bg-gradient-to-r from-green-400 to-blue-500">
        <nav class="flex justify-between py-4 px-6">
            <h1 class="text-xl text-white">
                <router-link to="/">Find a Coach</router-link>
            </h1>
            <ul class="list-none flex ">
                <li class="pr-4 text-white">
                    <router-link to="/coaches">All Coaches</router-link>
                </li>
                <li class="text-white">
                    <router-link to="/requests">Requests</router-link>
                </li>
            </ul>
        </nav>
    </header>
</template>