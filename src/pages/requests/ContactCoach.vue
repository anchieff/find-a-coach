<template>
    <form class="mt-5" @submit.prevent="submitForm">
        <div class="mb-4">
            <label for="email" class="form-label">Your E-Mail</label>
            <input
                type="email"
                class="form-input"
                id="email"
                v-model.trim="email"
            />
        </div>
        <div class="mb-3">
            <label for="message" class="form-label">Message</label>
            <textarea
                rows="5"
                class="form-input"
                id="message"
                v-model.trim="message"
            ></textarea>
        </div>
        <p class="text-red-600" v-if="!formIsValid">
            Please enter a valid email and non-empty message.
        </p>
        <div>
            <base-button mode="main">Send Message</base-button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            message: '',
            formIsValid: true,
        }
    },
    methods: {
        submitForm() {
            this.formIsValid = true
            if (
                this.email === '' ||
                !this.email.includes('@') ||
                this.message === ''
            ) {
                this.formIsValid = false
                return
            }
            this.$store.dispatch('requests/contactCoach', {
                email: this.email,
                message: this.message,
                coachId: this.$route.params.id,
            })
            this.$router.replace('/coaches')
        },
    },
}
</script>
