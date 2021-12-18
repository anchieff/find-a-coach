<template>
    <li class="border border-purple-300 rounded p-3 mb-4">
        <div>
            <a :href="emailLink" class="font-medium text-purple-800 mb-2">{{
                email
            }}</a>
        </div>
        <p>{{ message }}</p>
    </li>
</template>

<script>
export default {
    props: ['email', 'message'],
    computed: {
        emailLink() {
            return `mailto:${this.email}`
        },
    },
}
</script>
