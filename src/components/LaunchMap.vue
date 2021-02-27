<template>
  <div id="mapid">
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

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
            const mapDiv = L.map('mapid').setView(this.center, 5)
            L.tileLayer(
            "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
                {
                    attribution:
                        'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
                    maxZoom: 18,
                    id: "mapbox/streets-v11",
                    accessToken:"pk.eyJ1Ijoic2Vsc21pZSIsImEiOiJja2xub24zYmkwM2I3MndwaGd2cmphY2d0In0.pGKzXH4VZxv0ftDZvi4J4A",
                }
            ).addTo(mapDiv);
            L.circle(this.center, {color: 'red', radius: 100}).addTo(mapDiv);
        }
        
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