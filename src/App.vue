<template>
    <the-header></the-header>
    <hr />
    <div class="bg-gradient-to-b from-purple-50 to-white h-screen">
        <router-view v-slot="slotProps">
            <transition name="route" mode="out-in">
                <component :is="slotProps.Component"></component>
            </transition>
        </router-view>
    </div>
</template>

<script>
import TheHeader from './components/layout/TheHeader.vue'
export default {
    components: {
        TheHeader,
    },
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

.route-enter-from {
    opacity: 0;
    transform: translateY(-30px);
}
.route-leave-to {
    opacity: 0;
    transform: translateY(30px);
}
.route-enter-active {
    transition: all 0.3s easy-out;
}
.route-leave-active {
    transition: all 0.3s easy-in;
}
.route-enter-to,
.route-leave-from {
    opacity: 1;
    transform: translateY(0);
}
</style>
