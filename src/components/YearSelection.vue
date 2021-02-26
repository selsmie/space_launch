<template>
    <div>
        <label for="year">Year: </label>
        <input type="number" name="year" id="year" v-model='selectedYear'>
        <input type="submit" value="Search" v-on:click="handleYearSearch">
    </div>
  
</template>

<script>
import { eventBus } from '../main'
export default {
    name: 'year-selection',
    data() {
        return {
            selectedYear: null
        }
    },
    methods: {
        handleYearSearch() {
            eventBus.$emit('year-selected', this.selectedYear)
        }
    }
}
</script>

<style>

</style>