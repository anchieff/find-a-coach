<template>
    <section class="container mx-auto py-4">
        <coach-filter @change-filter="setFilters"></coach-filter>
    </section>
    <section class="container mx-auto">
        <base-card>
            <div class="flex justify-between">
                <base-button mode="secondary" class="mr-4" @click="loadCoaches">
                    Refresh
                </base-button>
                <base-button mode="main" v-if="!isCoach" link to="/register"
                    >Register as Coach</base-button
                >
            </div>
            <ul class="list-none mt-7" v-if="hasCoaches">
                <coach-item
                    v-for="coach in filteredCoaches"
                    :key="coach.id"
                    :id="coach.id"
                    :first-name="coach.firstName"
                    :last-name="coach.lastName"
                    :rate="coach.hourlyRate"
                    :areas="coach.areas"
                >
                </coach-item>
            </ul>
            <h3 v-else>No coaches found</h3>
        </base-card>
    </section>
</template>

<script>
import CoachItem from '../../components/coaches/CoachItem.vue'
import CoachFilter from '../../components/coaches/CoachFilter.vue'
export default {
    data() {
        return {
            activeFilters: {
                frontend: true,
                backend: true,
                career: true,
            },
        }
    },
    components: { CoachItem, CoachFilter },
    computed: {
        isCoach() {
            return this.$store.getters['coaches/isCoach']
        },
        filteredCoaches() {
            const coaches = this.$store.getters['coaches/coaches']
            return coaches.filter((coach) => {
                if (
                    this.activeFilters.frontend &&
                    coach.areas.includes('frontend')
                ) {
                    return true
                }
                if (
                    this.activeFilters.backend &&
                    coach.areas.includes('backend')
                ) {
                    return true
                }
                if (
                    this.activeFilters.career &&
                    coach.areas.includes('career')
                ) {
                    return true
                }
                return false
            })
        },
        hasCoaches() {
            return this.$store.getters['coaches/hasCoaches']
        },
    },
    methods: {
        setFilters(updatedFilters) {
            this.activeFilters = updatedFilters
        },
        loadCoaches() {
            this.$store.dispatch('coaches/loadCoaches')
        },
    },
    created() {
        this.loadCoaches()
    },
}
</script>
