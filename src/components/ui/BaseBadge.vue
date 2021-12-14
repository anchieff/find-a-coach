<template>
    <span class="px-4 py-2 rounded-3xl text-white bg-purple-800">
        {{ text }}
    </span>
</template>

<script>
export default {
    props: ['type', 'title'],
    computed: {
        text() {
            return this.title.toUpperCase()
        }
    }
}
</script>