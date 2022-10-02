<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        cart: {},
        editCartParams: {},
        errors: [],
        // message: {this.cart.name},
      };
    },
    created: function () {
      axios.get("/carts/" + this.$route.params.id).then((response) => {
        console.log("trucks show", response);
        this.cart = response.data;
        this.editCartParams = this.cart;
      });
    },
    methods: {
      updateCart: function (cart) {
        axios
          .patch("/carts/" + cart.id, this.editCartParams)
          .then((response) => {
            console.log("trucks update", response);
            this.$router.push("/carts");
          })
          .catch((error) => {
            console.log("carts update error", error.response);
            this.errors = error.response.data.errors;
          });
      },
    },
  };
  </script>
  
  <template>
    <div class="carts-edit">
      <h1>Edit Truck </h1>
      <!-- <p>{{message}}</p> -->
      <form v-on:submit.prevent="updateCart(cart)">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        Name:
        <input type="text" v-model="editCartParams.name" />
        Location:
        <input type="text" v-model="editCartParams.location" />
        Longitude:
        <input type="text" v-model="editCartParams.longitude" />
        Latitude:
        <input type="text" v-model="editCartParams.latitude" />
        Image_url:
        <input type="text" v-model="editCartParams.image_url" />
        <input type="submit" value="Update" />
      </form>
    </div>
  </template>
