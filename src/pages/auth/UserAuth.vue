<template>
    <div>
        <base-dialog
            :show="!!error"
            title="An error occured"
            @close="handleError"
        >
            <p>{{ error }}</p>
        </base-dialog>
        <base-dialog :show="isLoading" title="Authenticating..." fixed>
            <base-spinner></base-spinner>
        </base-dialog>
        <form class="pt-8" @submit.prevent="submitForm">
            <base-card>
                <div class="mb-3">
                    <label class="form-label" for="email">E-Mail</label>
                    <input
                        class="form-input"
                        type="email"
                        id="email"
                        v-model.trim="email"
                    />
                </div>
                <div class="mb-5">
                    <label class="form-label" for="password">Password</label>
                    <input
                        class="form-input"
                        type="password"
                        id="password"
                        v-model.trim="password"
                    />
                </div>
                <p v-if="!formIsValid" class="text-sm text-red-600">
                    Please enter a valid email and password (must be at least 6
                    characters long)
                </p>
                <div class="flex justify-end">
                    <base-button mode="main" class="mr-3">{{
                        submitButtonCaption
                    }}</base-button>
                    <base-button
                        type="button"
                        mode="secondary"
                        @click="switchAuthMode"
                        >{{ switchModeButtonCaption }}</base-button
                    >
                </div>
            </base-card>
        </form>
    </div>
</template>

<script>
import BaseDialog from '../../components/ui/BaseDialog.vue'
export default {
    components: { BaseDialog },
    data() {
        return {
            email: '',
            password: '',
            formIsValid: true,
            mode: 'login',
            isLoading: false,
            error: null,
        }
    },
    computed: {
        submitButtonCaption() {
            return this.mode === 'login' ? 'Login' : 'Signup'
        },
        switchModeButtonCaption() {
            return this.mode === 'login' ? 'Signup instead' : 'Login instead'
        },
    },
    methods: {
        async submitForm() {
            this.formIsValid = true
            if (
                this.email === '' ||
                !this.email.includes('@') ||
                this.password.length < 6
            ) {
                this.formIsValid = false
                return
            }

            this.isLoading = true
            const actionPayload = {
                email: this.email,
                password: this.password,
            }
            try {
                if (this.mode === 'login') {
                    await this.$store.dispatch('login', actionPayload)
                } else {
                    await this.$store.dispatch('signup', actionPayload)
                }
                const redirectUrl =
                    '/' + (this.$route.query.redirect || 'coaches')
                this.$router.replace(redirectUrl)
            } catch (err) {
                this.error = err.message || 'Failed to authenticate, try later.'
            }

            this.isLoading = false
        },
        switchAuthMode() {
            if (this.mode === 'login') {
                this.mode = 'signup'
            } else {
                this.mode = 'login'
            }
        },
        handleError() {
            this.error = null
        },
    },
}
</script>
