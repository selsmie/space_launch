<template>
  <main>
    <launch-list :launches='launches'></launch-list>
    <launch-details v-if="selectedLaunch" :launch='selectedLaunch'></launch-details>
  </main>
</template>

<script>
import LaunchList from './components/LaunchList'
import LaunchDetails from './components/LaunchDetails'
import {eventBus} from './main.js'

export default {
  name: "App",
  data() {
    return {
      launches: [],
      selectedLaunch: null,
    }
  },
  components: {
    "launch-list": LaunchList,
    "launch-details": LaunchDetails
  },
  methods: {
    getLaunchData: function() {
      fetch('https://lldev.thespacedevs.com/2.0.0/launch/?limit=100&offset=1650')
        .then(res => res.json())
        .then(data => this.launches = data.results)
    },
  },
  mounted() {
    this.getLaunchData()

    eventBus.$on('selected-launch', (launch) => this.selectedLaunch = launch)
  }
}
</script>

<style>

</style>