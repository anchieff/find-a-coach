<template>
    <span 
        class="px-4 py-2 rounded-full text-sm text-white"
        :class="{
            'bg-purple-800': type == 'frontend',
            'bg-yellow-500': type == 'career',
            'bg-green-600': type == 'backend'
        }"
    >
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