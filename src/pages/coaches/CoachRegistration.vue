<template>
    <section class="container mx-auto pt-8">
        <base-card>
            <h2 class="font-medium text-2xl mb-2">Register as a coach now!</h2>
            <coach-form @save-data="saveData"></coach-form>
        </base-card>
    </section>
</template>

<script>
import CoachForm from '../../components/coaches/CoachForm.vue'
export default {
    components: {
        CoachForm,
    },
    methods: {
        saveData(data) {
            this.$store.dispatch('coaches/registerCoach', data)
            this.$router.replace('/coaches')
        }
    }
}
</script>