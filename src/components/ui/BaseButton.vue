<template>
    <button v-if="!link" class="border-solid border-2 rounded px-5 py-1">
        <slot></slot>
    </button>
    <router-link v-else :to="to" class="border-solid border-2 rounded px-5 py-2">
        <slot></slot>
    </router-link>
</template>

<script>
export default {
    props: {
        mode: {
            type: String,
            required: false,
            default: null
        },
        link: {
            type: Boolean,
            required: false,
            default: false
        },
        to: {
            type: String,
            required: false,
            default: '/'
        }
    }
}
</script>