<template>
    <div>
        <base-dialog
            :show="!!error"
            title="An error occured!"
            @close="handleError"
        >
            {{ error }}
        </base-dialog>
        <section class="pt-8">
            <base-card>
                <header>
                    <h2 class="font-medium text-xl mb-3">Request Received</h2>
                </header>
                <div v-if="isLoading">
                    <base-spinner></base-spinner>
                </div>
                <ul v-else-if="hasRequests && !isLoading">
                    <request-item
                        v-for="request in receivedRequests"
                        :key="request.id"
                        :email="request.userEmail"
                        :message="request.message"
                    ></request-item>
                </ul>
                <h3 v-else class="font-medium">
                    You haven't received any request yet!
                </h3>
            </base-card>
        </section>
    </div>
</template>

<script>
import RequestItem from '../../components/requests/RequestItem.vue'
export default {
    components: {
        RequestItem,
    },
    data() {
        return {
            isLoading: false,
            error: null,
        }
    },
    computed: {
        receivedRequests() {
            return this.$store.getters['requests/requests']
        },
        hasRequests() {
            return this.$store.getters['requests/hasRequests']
        },
    },
    methods: {
        async loadRequests() {
            this.isLoading = true
            try {
                await this.$store.dispatch('requests/fetchRequests')
            } catch (err) {
                this.error = err.message || 'Something failed!'
            }

            this.isLoading = false
        },
        handleError() {
            this.error = null
        },
    },
    created() {
        this.loadRequests()
    },
}
</script>
