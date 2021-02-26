<template>
  <main>
    <div>
      <select v-model='filterData'>
        <option value="">All Launches</option>
        <option value="year">Year</option>
        <option value="status">Mission Status</option>
      </select>
    </div>

    <year-selection v-if="filterData==='year'"></year-selection>
    <status-selection v-if="filterData==='status'"></status-selection>

    <launch-list v-if="!filterData" :launches='launches'></launch-list>
    <launch-list v-if="filterData" :launches='filteredLaunches'></launch-list>
    <launch-details v-if="selectedLaunch" :launch='selectedLaunch'></launch-details>
  </main>
</template>

<script>
import LaunchList from './components/LaunchList'
import LaunchDetails from './components/LaunchDetails'
import YearSelection from './components/YearSelection'
import StatusSelection from './components/StatusSelection'

import {eventBus} from './main.js'

export default {
  name: "App",
  data() {
    return {
      launches: [],
      filteredLaunches: [],
      selectedLaunch: null,
      filterData: null
    }
  },
  components: {
    "launch-list": LaunchList,
    "launch-details": LaunchDetails,
    "year-selection": YearSelection,
    "status-selection": StatusSelection
  },
  methods: {
    getLaunchData: function() {
      fetch('https://lldev.thespacedevs.com/2.0.0/launch/?limit=100&offset=1650')
        .then(res => res.json())
        .then(data => this.launches = data.results)
    },
    dateYear: function(year) {
      this.launches.forEach((launch) => {
        if (launch.net.slice(0, 4) === year){
          this.filteredLaunches.push(launch)
        }
      })
    },
    statusMissions: function(status) {
      this.launches.forEach((launch) => {
        if (launch.status.name === status) {
          this.filteredLaunches.push(launch)
        }
      })
    }
  },
  mounted() {
    this.getLaunchData()

    eventBus.$on('selected-launch', (launch) => this.selectedLaunch = launch)
    
    eventBus.$on('reset', () => {
      this.launches = [],
      this.filteredLaunches = []
      })

    eventBus.$on('year-selected', (year) => this.dateYear(year))

    eventBus.$on('status-selected', (status) => this.statusMissions(status))
  }
}
</script>

<style>

</style>