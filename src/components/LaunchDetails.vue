<template>
    <section class='details'>
        <h2>{{launch.name}}</h2>
        <h3 class='status'>{{launch.status.name}}</h3>
        <img :src="launch.image" alt="">
        <p>Date: {{launch.net | date}}</p>
        <p id='obj'>Mission Objective</p>
        <p>{{launch.mission.description}}</p>
    </section>
</template>

<script>
export default {
    name: 'launch-details',
    props: ['launch'],
    filters: {
        date: function(dateString) {
            return new Date(dateString).toLocaleDateString()
        }
    },
}
</script>

<style>

.details {
    display: grid;
    grid-template-columns: 1fr;
    align-content: flex-start;
    justify-items: center;
    text-align: justify;
    /* width: 90%; */
    justify-self: end;
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