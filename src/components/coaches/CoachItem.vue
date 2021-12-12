<template>
    <li>
        <h3>{{ fullName }}</h3>
        <h4>${{ rate }}/hour</h4>
        <div>
            <base-badge v-for="area in areas" :key="area" :title="area" :type="area"></base-badge>
        </div>
        <div>
            <base-button link :to="coachContactLink">Contact</base-button>
            <base-button link :to="coachDetailsLink">View Details</base-button>
        </div>
    </li>
</template>

<script>
import BaseBadge from '../ui/BaseBadge.vue'
import BaseButton from '../ui/BaseButton.vue'
export default {
  components: { BaseButton, BaseBadge },
    props: ['id', 'firstName', 'lastName', 'rate', 'areas'],
    computed: {
        fullName() {
            return `${this.firstName} ${this.lastName}`
        },
        coachContactLink() {
            return `${this.$route.path}/${this.id}/contact`
        },
        coachDetailsLink() {
            return `${this.$route.path}/${this.id}`
        }
    }
}
</script>