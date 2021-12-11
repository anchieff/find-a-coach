<template>
    <the-header></the-header>
    <router-view></router-view>
</template>

<script>
import TheHeader from './components/layout/TheHeader.vue'
export default {
    components: {
        TheHeader
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap');

* {
    box-sizing: border-box;
}
body {
    margin: 0;
    padding: 0;
    font-family: 'Montserrat', sans-serif;
}
</style>