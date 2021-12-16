<template>
    <the-header></the-header>
    <hr/>
    <div class="bg-gradient-to-b from-purple-50 to-white">
        <router-view></router-view>
    </div>
    
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
    font-size: 16px;
}
</style>