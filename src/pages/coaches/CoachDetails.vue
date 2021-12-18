<template>
    <section class="pt-8 mb-5">
        <base-card class="pb-5">
            <h2 class="text-2xl mb-3">{{ fullName }}</h2>
            <h3 class="text-xl mb-4">${{ rate }}/hour</h3>
        </base-card>
    </section>
    <section class="mb-5">
        <base-card>
            <header>
                <h2 class="font-medium text-xl mb-3">
                    Interested? Reach out now!
                </h2>
                <base-button mode="secondary" link :to="coachContactLink">
                    Contact
                </base-button>
            </header>
            <router-view></router-view>
        </base-card>
    </section>
    <section>
        <base-card>
            <base-badge
                v-for="area in areas"
                :key="area"
                :title="area"
                :type="area"
                class="mr-3"
            ></base-badge>
            <p class="mt-4">{{ description }}</p>
        </base-card>
    </section>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            selectedCoach: null,
        }
    },
    computed: {
        fullName() {
            return `${this.selectedCoach.firstName} ${this.selectedCoach.lastName}`
        },
        coachContactLink() {
            return `${this.$route.path}/contact`
        },
        rate() {
            return this.selectedCoach.hourlyRate
        },
        areas() {
            return this.selectedCoach.areas
        },
        description() {
            return this.selectedCoach.description
        },
    },
    created() {
        this.selectedCoach = this.$store.getters['coaches/coaches'].find(
            (coach) => coach.id == this.id
        )
    },
}
</script>
