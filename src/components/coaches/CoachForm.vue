<template>
    <form @submit.prevent="submitForm">
        <div class="mb-3">
            <label
                class="form-label"
                for="firstname"
                :class="{ 'error-label': !firstName.isValid }"
            >
                Firstname
            </label>
            <input
                class="form-input"
                :class="{ 'error-input': !firstName.isValid }"
                type="text"
                id="firstname"
                v-model.trim="firstName.val"
                @blur="clearValidity('firstName')"
            />
            <p class="text-sm text-red-600 mt-1" v-if="!firstName.isValid">
                Firstname must not be empty
            </p>
        </div>

        <div class="mb-3">
            <label
                class="form-label"
                :class="{ 'error-label': !lastName.isValid }"
                for="lastname"
            >
                Lastname
            </label>
            <input
                class="form-input"
                :class="{ 'error-input': !lastName.isValid }"
                type="text"
                id="lastname"
                v-model.trim="lastName.val"
                @blur="clearValidity('lastName')"
            />
            <p class="text-sm text-red-600 mt-1" v-if="!lastName.isValid">
                Lastname must not be empty
            </p>
        </div>

        <div class="mb-3">
            <label
                class="form-label"
                :class="{ 'error-label': !description.isValid }"
                for="description"
            >
                Description
            </label>
            <textarea
                class="form-input"
                :class="{ 'error-input': !description.isValid }"
                id="description"
                rows="5"
                v-model.trim="description.val"
                @blur="clearValidity('description')"
            ></textarea>
            <p class="text-sm text-red-600 mt-1" v-if="!description.isValid">
                Description must not be empty
            </p>
        </div>

        <div class="mb-3">
            <label
                class="form-label"
                :class="{ 'error-label': !rate.isValid }"
                for="rate"
            >
                Hourly rate
            </label>
            <input
                class="form-input"
                :class="{ 'error-input': !rate.isValid }"
                type="number"
                id="rate"
                v-model.number="rate.val"
                @blur="clearValidity('rate')"
            />
            <p class="text-sm text-red-600 mt-1" v-if="!rate.isValid">
                Rate must be greater than 0.
            </p>
        </div>

        <div class="mb-5">
            <h3 class="form-label" :class="{ 'error-label': !areas.isValid }">
                Areas of Expertise
            </h3>
            <div>
                <input
                    class="mr-2"
                    type="checkbox"
                    id="frontend"
                    value="frontend"
                    v-model="areas.val"
                    @blur="clearValidity('areas')"
                />
                <label for="frontend">Frontend Development</label>
            </div>
            <div>
                <input
                    class="mr-2"
                    type="checkbox"
                    id="backend"
                    value="backend"
                    v-model="areas.val"
                    @blur="clearValidity('areas')"
                />
                <label for="backend">Backend Development</label>
            </div>
            <div>
                <input
                    class="mr-2"
                    type="checkbox"
                    id="career"
                    value="career"
                    v-model="areas.val"
                    @blur="clearValidity('areas')"
                />
                <label for="career">Career Advisory</label>
            </div>
            <p class="text-sm text-red-600 mt-1" v-if="!areas.isValid">
                At least one expertise must be select
            </p>
        </div>
        <p class="mb-3" v-if="!formIsValid">
            Please fix the above errors and submit again.
        </p>
        <base-button mode="main">Register</base-button>
    </form>
</template>

<script>
export default {
    emits: ['save-data'],
    data() {
        return {
            firstName: {
                val: '',
                isValid: true,
            },
            lastName: {
                val: '',
                isValid: true,
            },
            description: {
                val: '',
                isValid: true,
            },
            rate: {
                val: null,
                isValid: true,
            },
            areas: {
                val: [],
                isValid: true,
            },
            formIsValid: true,
        }
    },
    methods: {
        clearValidity(input) {
            this[input].isValid = true
        },
        validateForm() {
            this.formIsValid = true

            if (this.firstName.val === '') {
                this.firstName.isValid = false
                this.formIsValid = false
            }

            if (this.lastName.val === '') {
                this.lastName.isValid = false
                this.formIsValid = false
            }

            if (this.description.val === '') {
                this.description.isValid = false
                this.formIsValid = false
            }

            if (!this.rate.val || this.rate.val < 0) {
                this.rate.isValid = false
                this.formIsValid = false
            }

            if (this.areas.val.length === 0) {
                this.areas.isValid = false
                this.formIsValid = false
            }
        },
        submitForm() {
            this.validateForm()

            if (!this.formIsValid) {
                return
            }

            const formData = {
                first: this.firstName.val,
                last: this.lastName.val,
                desc: this.description.val,
                rate: this.rate.val,
                areas: this.areas.val,
            }
            this.$emit('save-data', formData)
        },
    },
}
</script>
