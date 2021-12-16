<template>
    <form @submit.prevent="submitForm">
        <div>
            <label for="firstname">Firstname</label>
            <input type="text" id="firstname" v-model.trim="firstName" />
        </div>
        <div>
            <label for="lastname">Lastname</label>
            <input type="text" id="lastname" v-model.trim="lasttName" />
        </div>
        <div>
            <label for="description">Description</label>
            <textarea id="description" rows="5" v-model.trim="description"></textarea>
        </div>
        <div>
            <label for="rate">Hourly rate</label>
            <input type="number" id="rate" v-model.number="rate" />
        </div>
        <div>
            <h3>Areas of Expertise</h3>
            <div>
                <input type="checkbox" id="frontend" value="frontend" v-model="areas"/>
                <label for="frontend">Frontend Development</label>
            </div>
            <div>
                <input type="checkbox" id="backend" value="backend" v-model="areas"/>
                <label for="backend">Backend Development</label>
            </div>
            <div>
                <input type="checkbox" id="career" value="career" v-model="areas"/>
                <label for="career">Career Advisory</label>
            </div>
        </div>
        <base-button>Register</base-button>
    </form>
</template>

<script>
export default {
    emits: ['save-data'],
    data() {
        return {
            firstName: '',
            lastName: '',
            description: '',
            rete: null,
            areas: []
        }
    },
    methods: {
        submitForm() {
            const formData = {
                first: this.firstName,
                last: this.lastName,
                desc: this.description,
                rate: this.rate,
                areas: this.areas
            }
            this.$emit('save-data', formData)
        }
    }
}
</script>