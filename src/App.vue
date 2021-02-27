<template>
  <main>
    <h1>Rocket Launches</h1>
    <div class='filter-area'>
      <select v-model='filterData' v-on:change='selectedLaunch=null'>
        <option disabled value="">Select Launches</option>
        <option value="all">All Launches</option>
        <option value="year">Year</option>
        <option value="status">Mission Status</option>
      </select>
   
      <year-selection v-if="filterData==='year'"></year-selection>
      <status-selection v-if="filterData==='status'"></status-selection>
    </div>

   
    <section>
      <launch-list v-if="filterData==='all'" :launches='launches'></launch-list>
      <launch-list v-if="filterData==='year' || filterData==='status'" :launches='filteredLaunches'></launch-list>
      <launch-details v-if="selectedLaunch" :launches='launches' :index='selectedLaunchIndex'></launch-details>
    </section>
    
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
      filterData: null,
      selectedLaunchIndex: null
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
      fetch('https://lldev.thespacedevs.com/2.0.0/launch/?limit=100&offset=1600')
        .then(res => res.json())
        .then(data => this.launches = data.results)
    },

    dateYear: function(year) {
      this.filteredLaunches = []
      this.launches.forEach((launch) => {
        if (launch.net.slice(0, 4) === year){
          this.filteredLaunches.push(launch)
        }
      })
    },
    statusMissions: function(status) {
      this.filteredLaunches = []
      this.launches.forEach((launch) => {
        if (launch.status.name === status) {
          this.filteredLaunches.push(launch)
        }
      })
    },
    selectedLaunchId: function() {
      this.selectedLaunchIndex = this.launches.indexOf(this.selectedLaunch)
    },
    selectedIdNext: function() {
      this.selectedLaunchIndex++
    },
    selectedIdBack: function() {
      this.selectedLaunchIndex--
    }
  },
  mounted() {
    this.getLaunchData()

    eventBus.$on('selected-launch', (launch) => (this.selectedLaunch = launch, this.selectedLaunchId(), this.index = null))
    eventBus.$on('year-selected', (year) => this.dateYear(year))
    eventBus.$on('status-selected', (status) => this.statusMissions(status))
    eventBus.$on('skip-next', () => (this.selectedIdNext()))
    eventBus.$on('skip-back', () => (this.selectedIdBack()))
  }
}
</script>

<style>
body {
  box-sizing: border-box;
  background-image: url("https://cdn.mos.cms.futurecdn.net/xePTkUayyCCn7QnVXUjhTg.jpg");
  margin: 0;
  height: 100%;
}

main {
  height: 100%;
  margin: 15px;
  color: white;
}

h1 {
  text-align: center;
  margin: 0px;
}

.filter-area {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 41px;
}

section {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  column-gap: 25px;
}

select {
  border-radius: 12px;
  height: 30px;
  padding-left: 5px;
}
</style>