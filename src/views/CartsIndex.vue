<script>
  import axios from "axios";
  import mapboxgl from 'mapbox-gl'; // or "const mapboxgl = require('mapbox-gl');"

  export default {
    data: function () {
      return {
        message: "All Trucks",
        carts: [],
        shortestRoutes: [],
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
          // Add geolocate control to the map.
          map.addControl(
          new mapboxgl.GeolocateControl({
          positionOptions: {
          enableHighAccuracy: true
          },
          // When active the map will receive updates to the device's location as it changes.
          trackUserLocation: true,
          // Draw an arrow next to the location dot to indicate which direction the device is heading.
          showUserHeading: true
          })
          );
        })
      },
      indexShortestRoutes: function () {
        axios.get("/shortest_routes").then((response) => {
          console.log('getting routes', response);
          this.shortestRoutes = response.data;
          mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
      });
    },
      makeMap: function() {
      }
    },
  };
</script>

<template>
  <div class="carts-index">
    <h4>{{ shortestRoutes }}</h4>
    <button v-on:click="indexShortestRoutes">Find Nearest Taco Truck</button>
    <ul class="actions">
            <li><a href="/" class="button scrolly">Return to Home Screen</a></li>
          </ul>
          <!-- <ul class="actions">
         <li><a href="/carts" class="button scrolly">Find Taco Truck</a></li>
          </ul> -->
    <div id='map' style='width: 880px; height: 660px;'></div>
  </div>
</template>
<style></style>
