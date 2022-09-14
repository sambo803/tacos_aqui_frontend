
<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        message: "iTacos Aqui!",
        carts: [],
      };
    },
    created: function () {
      process.env.VUE_APP_MAPBOX_API_KEY;
      this.indexCarts();
    },
    methods: {
      indexCarts: function () {
        axios.get("/carts").then((response) => {
          console.log('getting carts', response);
          this.carts = response.data;
        })
      }
    },
  };
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="cart in carts" v-bind:key="cart.id">
    <h2>{{cart.name}}</h2>
    <!-- <img v-bind:src="cart.image_url" v-bind:alt="cart.name" /> -->
  </div>
  </div>
</template>

<style></style>
