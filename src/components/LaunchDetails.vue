<template>
<section class='details-area'>
    <section class='details' v-if=!nextIndex>
            <h2>{{launch.name}}</h2>
            <h3 class='status'>{{launch.status.name}}</h3>
            <img :src="launch.image" alt="">
            <p>Date: {{launch.net | date}}</p>
            <p id='obj'>Mission Objective</p>
            <p>{{launch.mission.description}}</p>
        <span><button v-on:click="skipBack"><< Previous</button><button v-on:click="skipNext">Next >></button></span>
    </section>
    <section class='details' v-if=nextIndex>
            <h2>{{launches[nextIndex].name}}</h2>
            <h3 class='status'>{{launches[nextIndex].status.name}}</h3>
            <img :src="launches[nextIndex].image" alt="">
            <p>Date: {{launches[nextIndex].net | date}}</p>
            <p id='obj'>Mission Objective</p>
            <p>{{launches[nextIndex].mission.description}}</p>
        <span><button v-on:click="skipBack"><< Previous</button><button v-on:click="skipNext">Next >></button></span>
    </section>
</section>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: 'launch-details',
    props: ['launch', 'nextIndex', 'launches'],
    filters: {
        date: function(dateString) {
            return new Date(dateString).toLocaleDateString()
        }
    },
    methods: {
        skipNext: function(){
            eventBus.$emit('skip-next', this.launch)
        },
        skipBack: function() {
            eventBus.$emit('skip-back', this.launch)
        }
    }
}
</script>

<style>

.details-area{
    display: grid;
    grid-template-columns: 1fr;
}

.details {
    display: grid;
    grid-template-columns: 1fr;
    align-content: flex-start;
    justify-items: center;
    text-align: justify;
    /* width: 90%; */
    justify-self: center;
}

.status {
    margin-top: 0px;
}

#obj {
    margin: 0;
    font-weight: bold;
    text-decoration: underline;
}

img {
    width: auto;
    height: auto;
    max-height: 300px;
    max-width: 300px;
}
</style>