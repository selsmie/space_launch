<template>
  <div id="mapid">
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import { my_key } from '../config.js'

export default {
    name: 'Map',
    props: ['launch'],
    data () {
        return{
            center: [this.launch.pad.latitude, this.launch.pad.longitude],
        }
    },
    methods: {
        setUpMap: function() {
            const mapDiv = L.map('mapid').setView(this.center, 7)
            L.tileLayer(
            "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=" + my_key,
                {
                    attribution:
                        'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
                    maxZoom: 18,
                    id: "mapbox/streets-v11",
                }
            ).addTo(mapDiv);

            delete L.Icon.Default.prototype._getIconUrl  
            L.Icon.Default.mergeOptions({  
                iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),  
                iconUrl: require('leaflet/dist/images/marker-icon.png'),  
                shadowUrl: require('leaflet/dist/images/marker-shadow.png')  
            })


            L.marker(this.center).addTo(mapDiv);
        },

        
        
    },
    mounted() {
        this.setUpMap()
    }
}
</script>

<style>
#mapid {
    height: 400px;
    width: 100%;
    margin-top: 10px;
}
</style>