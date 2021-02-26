<template>
<section class='details-area'>
    <section class='details'>
            <h2 class='title'>{{launches[index].name}}</h2>
            <h3 class='status'>{{launches[index].status.name}}</h3>
            <img :src="launches[index].image" alt="">
            <p id='date'>Date: {{launches[index].net | date}}</p>
            <h3 class='company'>{{launches[index]['launch_service_provider'].name}}</h3 class='company'>
            <p id='obj'>Mission Brief</p>
            <p id='description'>{{launches[index].mission.description}}</p>
    </section>
    <footer>
        <button v-if="index > 0" v-on:click="skipBack"><< Previous</button>
        <button>Launch Map</button>
        <button v-if="index < 99" v-on:click="skipNext">Next >></button>
    </footer>
</section>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: 'launch-details',
    props: ['launch', 'launches', 'index'],
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
    max-height: 300px;
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