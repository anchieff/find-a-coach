<template>
    <li class="mt-7">
        <h3 class="text-2xl mb-3">{{ fullName }}</h3>
        <h4 class="text-xl mb-4">${{ rate }}/hour</h4>
        <div class="mb-7">
            <base-badge v-for="area in areas" :key="area" :title="area" :type="area" class="mr-3"></base-badge>
        </div>
        <div>
            <base-button class="mr-3" link :to="coachContactLink">Contact</base-button>
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