<template>
    <span :class="mode">
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