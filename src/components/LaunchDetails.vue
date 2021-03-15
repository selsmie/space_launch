<template>
<section class='details-area'>
    <section class='details'>
            <h2 class='title'>{{launches[index].name}}</h2>
            <h3 class='status'>{{launches[index].status.name}}</h3>
            <img :src="launches[index].image" alt="">
            <p id='date'>Date: {{launches[index].net | date}}</p>
            <h3 class='company'>{{launches[index]['launch_service_provider'].name}}</h3>
            <p id='obj'>Mission Brief</p>
            <p id='description' v-if='!showMap'>{{launches[index].mission.description}}</p>
            <launch-map v-if='showMap' :launch="launches[index]"></launch-map>
    </section>
    
    <footer>
        <button v-if="index > 0" v-on:click="skipBack"><< Previous</button>
        <button v-on:click="showMapClick">Launch Map</button>
        <button v-if="index < 199" v-on:click="skipNext">Next >></button>
    </footer>
     
</section>
</template>

<script>
import { eventBus } from '../main.js'
import LaunchMap from './LaunchMap'

export default {
    name: 'launch-details',
    data() {
        return {
            showMap: false
        }
    },
    props: ['launch', 'launches', 'index'],
    components: {'launch-map': LaunchMap},
    filters: {
        date: function(dateString) {
            return new Date(dateString).toLocaleDateString()
        }
    },
    methods: {
        skipNext: function(){
            eventBus.$emit('skip-next', this.launch)
            this.showMap = false
        },
        skipBack: function() {
            eventBus.$emit('skip-back', this.launch)
            this.showMap = false
        },
        showMapClick: function(){
            if (!this.showMap) {
                this.showMap = true
            } else {
                this.showMap = false
            }
        },
    },
    mounted() {
        eventBus.$on('restore-display', () => this.showMap = false)
    }
}
</script>

<style>

.details-area{
    display: grid;
    grid-template-columns: 1fr;
}

.details::-webkit-scrollbar {
  display: none;
}

.title {
    text-align: center;
}

.details {
    display: grid;
    grid-template-columns: 1fr;
    align-content: flex-start;
    justify-items: center;
    text-align: justify;
    height: 83vh;
    width: 80%;
    justify-self: center;
    overflow: scroll;
}

#description::-webkit-scrollbar {
  display: none;
}

.status {
    margin: 0px;
}

#date {
    margin: 5px 0px 0px 0px;
}

.company{
    margin: 5px;
    text-align: center;
}

#description{
    margin: 5px 0px;
    overflow: scroll;
}

#obj {
    margin: 0;
    font-weight: bold;
    text-decoration: underline;
}

img {
    width: auto;
    height: auto;
    max-height: 200px;
    max-width: 300px;
}

footer {
    justify-self: center;
    align-self: flex-end;
}

footer > button {
    height: 40px;
    width: 120px;
    margin: 0px 30px;
    border-radius: 12px;
}
</style>