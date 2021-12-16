<template>
    <header class="container mx-auto">
        <nav class="flex justify-between items-start py-4 px-6">
            <h1 class="text-xl font-medium text-purple-900">
                <router-link to="/">Find a Coach</router-link>
            </h1>
            <ul class="list-none flex ">
                <li class="pr-4 ">
                    <router-link to="/coaches">All Coaches</router-link>
                </li>
                <li>
                    <router-link to="/requests">Requests</router-link>
                </li>
            </ul>
        </nav>
    </header>
</template>