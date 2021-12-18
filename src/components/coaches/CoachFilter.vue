<template>
    <base-card>
        <h2 class="font-medium text-xl mb-2">Find Your Coach</h2>
        <span class="mr-2">
            <input type="checkbox" id="frontend" checked @change="setFilters"/>
            <label for="frontend" class="text-l ml-1">Frontend</label>
        </span>
        <span class="mr-2">
            <input type="checkbox" id="backend" checked @change="setFilters"/>
            <label for="backend" class="text-l ml-1">Backend</label>
        </span>
        <span>
            <input type="checkbox" id="career" checked @change="setFilters"/>
            <label for="career" class="text-l ml-1">Career</label>
        </span>
    </base-card>
</template>

<script>
export default {
    emits: ['change-filter'],
    data() {
        return {
            filters: {
                frontend: true,
                backend: true,
                career: true
            }
        }
    },
    methods: {
        setFilters(event) {
            const inputId = event.target.id
            const isActive = event.target.checked
            const updatedFilters = {
                ...this.filters,
                [inputId]: isActive
            }
            this.filters = updatedFilters
            this.$emit('change-filter', updatedFilters)
        }
    }
}
</script>