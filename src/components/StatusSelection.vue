<template>
    <div>
        <label for="year">Status: </label>
        <select v-model="selectedStatus">
            <option disabled value="">Select a status</option>
            <option value="Success">Success</option>
            <option value="Failure">Failure</option>
            <option value="Partial Failure">Partial Failure</option>
        </select>
        <input type="submit" value="Search" v-on:click="handleStatusSearch">
    </div>
  
</template>

<script>
import { eventBus } from '../main'
export default {
    name: 'status-selection',
    data() {
        return {
            selectedStatus: null
        }
    },
    methods: {
        handleStatusSearch() {
            eventBus.$emit('status-selected', this.selectedStatus)
        }
    }
}
</script>

<style>

</style>