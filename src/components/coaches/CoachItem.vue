<template>
    <li class="mt-5 border-2 border-purple-800 rounded p-8">
        <h3 class="text-2xl mb-3">{{ fullName }}</h3>
        <h4 class="text-xl mb-4">${{ rate }}/hour</h4>
        <div class="mb-9">
            <base-badge v-for="area in areas" :key="area" :title="area" :type="area" class="mr-2"></base-badge>
        </div>
        <div class="flex justify-end">
            <base-button mode="main" class="mr-2" link :to="coachContactLink">Contact</base-button>
            <base-button mode="secondary" link :to="coachDetailsLink">View Details</base-button>
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