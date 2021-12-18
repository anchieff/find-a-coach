<template>
    <section class="pt-8">
        <base-card>
            <header>
                <h2 class="font-medium text-xl mb-3">Request Received</h2>
            </header>
            <ul v-if="hasRequests">
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
</template>

<script>
import RequestItem from '../../components/requests/RequestItem.vue'
export default {
    components: {
        RequestItem,
    },
    computed: {
        receivedRequests() {
            return this.$store.getters['requests/requests']
        },
        hasRequests() {
            return this.$store.getters['requests/hasRequests']
        },
    },
}
</script>
