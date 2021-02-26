<template>
    <section>
        <h2>{{launch.name}}</h2>
        <h3>{{launch.status.name}}</h3>
        <img :src="launch.image" alt="">
        <p>Date: {{launch.net | date}}</p>
        <p>Mission: {{launch.mission.description}}</p>
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
img {
    height: 200px;
}
</style>