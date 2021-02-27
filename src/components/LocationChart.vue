<template>
  <GChart type='PieChart' :data='chartData' :options="chartOptions"/>
</template>

<script>
import { GChart } from 'vue-google-charts'

export default {
    name: 'location-chart',
    data() {
      return {
        chartOptions: {
          title: 'Launch Locations by Country',
          legend: {position: 'right'},
          height: 400,
          width: 700,
         
          chartArea: {left:140, top:40,width: '100%', height: '100%'},
          pieSliceText: 'value'
        },
        locationsArray: [],
        nestedLocations: [],
      }
    },
    components: { GChart },
    props: ['launches'],
    methods: {
        launchLocations: function(){
            const set = new Set(this.launches.map((launch) => launch.pad.location['country_code']))
            this.locationsArray = Array.from(set)
        },
        launchLocationsNested: function(){
            this.locationsArray.forEach((location) => {
                return this.nestedLocations.push([location])
            })
        },
        locationCount: function() {
            this.nestedLocations.map((location) => {
                let counter = 0
                this.launches.map((launch) => {
                    if(location[0] === launch.pad.location['country_code']) {
                        counter++
                    }
                })
                location.push(counter)
            })
        },
    },
    computed: {
        chartData: function() {
            const chartData = [['country', 'total'], ...this.nestedLocations]
            return chartData
      },
    },
    mounted() {
        this.launchLocations()
        this.launchLocationsNested()
        this.locationCount()
    }
}
</script>

<style>

</style>