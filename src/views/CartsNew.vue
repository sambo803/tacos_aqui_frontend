<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        newCartParams: {},
        errors: [],
        // message: {this.cart.name},
      };
    },
    created: function (){},
    methods: {
      createCart: function () {
        axios.post("/carts", this.newCartParams).then((response) => {
        console.log("trucks create", response);
        this.$router.push("/carts");
      })
      .catch((error) => {
        console.log("carts create error", error.response);
        this.errors = error.response.data.errors;
      });
      },
    },
  };
  </script>
  
  <template>
    <div class="carts-new">
      <h1>New Truck </h1>
      <!-- <p>{{message}}</p> -->
      <form v-on:submit.prevent="createCart()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        Name:
        <input type="text" v-model="newCartParams.name" />
        Location:
        <input type="text" v-model="newCartParams.location" />
        Longitude:
        <input type="text" v-model="newCartParams.longitude" />
        Latitude:
        <input type="text" v-model="newCartParams.latitude" />
        Email:
        <input type="text" v-model="newCartParams.email" />
        Phone_number:
        <input type="text" v-model="newCartParams.phone_number" />
        <input type="submit" value="Create" />
      </form>
    </div>
  </template>