<template>
    <button
        v-if="!link"
        class="border-solid border-2 rounded px-5 py-2 font-medium"
        :class="{
            'btn-secondary': mode === 'secondary',
            'btn-primary': mode === 'main',
            'btn-flat': mode === 'flat',
        }"
    >
        <slot></slot>
    </button>
    <router-link
        v-else
        :to="to"
        class="border-solid border-2 rounded px-5 py-2 font-medium"
        :class="{
            'btn-secondary': mode === 'secondary',
            'btn-primary': mode === 'main',
            'btn-flat': mode === 'flat',
        }"
    >
        <slot></slot>
    </router-link>
</template>

<script>
export default {
    props: {
        mode: {
            type: String,
            required: false,
            default: null,
        },
        link: {
            type: Boolean,
            required: false,
            default: false,
        },
        to: {
            type: String,
            required: false,
            default: '/',
        },
    },
}
</script>
