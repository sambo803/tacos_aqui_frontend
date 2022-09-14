<script>
  import axios from "axios";
  import mapboxgl from 'mapbox-gl'; // or "const mapboxgl = require('mapbox-gl');"

  export default {
    data: function () {
      return {
        message: "All Carts",
        carts: [],
      };
    },
    created: function () {
      this.indexCarts();
    },
    mounted: function () {
      
      this.makeMap();
    },
    methods: {
      indexCarts: function () {
        axios.get("/carts").then((response) => {
          console.log('getting carts', response);
          this.carts = response.data;
        })
      },
      makeMap: function() {
        mapboxgl.accessToken =process.env.VUE_APP_MAPBOX_API_KEY;
        const map = new mapboxgl.Map({
        container: 'map', // container ID
        style: 'mapbox://styles/mapbox/streets-v11', // style URL
        center: [-74.5, 40], // starting position [lng, lat]
        zoom: 9, // starting zoom
        projection: 'globe' // display the map as a 3D globe
        });
        map.on('style.load', () => {
        map.setFog({}); // Set the default atmosphere style
        });
      }
    },
  };
</script>

<template>


  <div class="carts-index">
    <h1>{{ message }}</h1>
    <button v-on:click="makeMap()">Make Map</button>
    <div id='map' style='width: 400px; height: 300px;'></div>
    <h2>{{ Map }}</h2>
    <!-- <div>{{carts}}</div> -->
  
  </div>

</template>

<style></style>
