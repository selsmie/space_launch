<template>
  <li v-on:click='handleClick'>{{launch.name}} - {{launch.net | year}}</li>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'launch-item',
    props: ['launch'],
    filters: {
        year: function(dateString) {
            return new Date(dateString).getFullYear()
        }
    },
    methods: {
        handleClick() {
            eventBus.$emit('selected-launch', this.launch)
            eventBus.$emit('restore-display')
        }
    }
}
</script>

<style>
li {
    cursor: pointer;
}

li:hover{
    color: red;
}
</style>