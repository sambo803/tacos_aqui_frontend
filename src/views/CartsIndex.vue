<script>
  import axios from "axios";
  import mapboxgl from 'mapbox-gl'; // or "const mapboxgl = require('mapbox-gl');"

  export default {
    data: function () {
      return {
        message: "All Trucks",
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
          mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
        const map = new mapboxgl.Map({
        container: 'map', // container ID
        style: 'mapbox://styles/mapbox/streets-v11', // style URL
        center: [-104.94338204397512, 39.74742474125658], // starting position [lng, lat]
        zoom: 9, // starting zoom
        projection: 'globe' // display the map as a 3D globe
        });
        map.on('style.load', () => {
        map.setFog({}); // Set the default atmosphere style
        });
          this.carts = response.data;
          console.log(this.carts);
          this.carts.forEach(cart => {
            const marker1 = new mapboxgl.Marker()
          .setLngLat([cart.longitude, cart.latitude])
          .addTo(map)
          });

        })
      },
      makeMap: function() {

      }
    },
  };
</script>

<template>


  <div class="carts-index">
    <h1>{{ message }}</h1>
    <!-- <button v-on:click="makeMap()">Make Map</button> -->
    <div id='map' style='width: 880px; height: 660px;'></div>
    <!-- <h2>{{ Map }}</h2> -->
    <!-- <div>{{carts}}</div> -->
  
  </div>

</template>

<style></style>
