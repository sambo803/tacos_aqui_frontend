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
        // 1- senor miguel's marker
        const marker1 = new mapboxgl.Marker({ color: 'green', rotation: 45 })
        .setLngLat([-105.02557184503674, 39.729430831758876])
        .addTo(map);
        // 2- sally's 
        const marker2 = new mapboxgl.Marker({ color: 'black', rotation: 45 })
        .setLngLat([-105.04410465714048, 39.74027577412321])
        .addTo(map);
        // 3-Tacos Jaliscos
        const marker3 = new mapboxgl.Marker({ color: 'red', rotation:   45 })
        .setLngLat([-104.99546343634663, 39.754971979447596])
        .addTo(map);
        // 4-Ruby's Treats
        const marker4 = new mapboxgl.Marker({ color: 'Blue', rotation:   45 })
        .setLngLat([-105.02328190583546, 39.75115333332979])
        .addTo(map);
        // 5-Ronaldo's Tamales
        const marker5 = new mapboxgl.Marker({ color: 'pink', rotation:   45 })
        .setLngLat([-105.01112109060736, 39.776510929891074])
        .addTo(map);
        // 6-Chinti's Burritos
        const marker6 = new mapboxgl.Marker({ color: 'orange', rotation:   45 })
        .setLngLat([-104.77208641547043, 39.69678852815054])
        .addTo(map);
      }
    },
  };
</script>

<template>


  <div class="carts-index">
    <h1>{{ message }}</h1>
    <!-- <button v-on:click="makeMap()">Make Map</button> -->
    <div id='map' style='width: 400px; height: 300px;'></div>
    <!-- <h2>{{ Map }}</h2> -->
    <!-- <div>{{carts}}</div> -->
  
  </div>

</template>

<style></style>
