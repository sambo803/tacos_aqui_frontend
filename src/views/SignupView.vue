<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        newOwnerParams: {},
        errors: [],
      };
    },
    methods: {
      submit: function () {
        axios
          .post("/owners", this.newOwnerParams)
          .then((response) => {
            console.log(response.data);
            this.$router.push("/login");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      },
    },
  };
</script>

<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newOwnerParams.name" />
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newOwnerParams.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newOwnerParams.password" />
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newOwnerParams.password_confirmation" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>