
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
    <!-- Intro -->
      <section id="intro" class="wrapper style1 fullscreen fade-up">
        <div class="inner">
          <h1>Tacos Aqui! Home</h1>
          <p>Taco Trucks Near You</p>
          <ul class="actions">
            <li><a href="/carts" class="button scrolly">See Map</a></li>
          </ul>
        </div>
      </section>

    <!-- One -->
      <section id="one" class="wrapper style2 spotlights">
        <section v-for="cart in carts" v-bind:key="cart.id">
          <a href="/carts" class="image"><img v-bind:src="cart.image_url"  style='width: 600px; height: 440px;' data-position="center center" /></a>
          <div class="content">
            <div class="inner">
              <h2>{{cart.name}}</h2>
              <p>{{ cart.location }}</p>
            </div>
          </div>
        </section>
      </section>

    <!-- Three -->
      <section id="three" class="wrapper style1 fade-up">
        <div class="inner">
          <h2>Owners Login/ Signup</h2>
          <div class="split style1">
            <section>
              <form method="post" action="#">
                <div class="fields">
                  <div class="field half">
                    <label for="name">Name</label>
                    <input type="text" name="name" id="name" />
                  </div>
                  <div class="field half">
                    <label for="email">Email</label>
                    <input type="text" name="email" id="email" />
                  </div>
                  <div class="field">
                    <label for="message">Message</label>
                    <textarea name="message" id="message" rows="5"></textarea>
                  </div>
                </div>
                <ul class="actions">
                  <li><a href="" class="button submit">Send Message</a></li>
                </ul>
              </form>
            </section>
            <section>
              <ul class="contact">
                <li>
                  <h3>Address</h3>
                  <span>12345 Somewhere Road #654<br />
                  Nashville, TN 00000-0000<br />
                  USA</span>
                </li>
                <li>
                  <h3>Email</h3>
                  <a href="#">user@untitled.tld</a>
                </li>
                <li>
                  <h3>Phone</h3>
                  <span>(000) 000-0000</span>
                </li>
                <li>
                  <h3>Social</h3>
                  <ul class="icons">
                    <li><a href="#" class="icon brands fa-twitter"><span class="label">Twitter</span></a></li>
                    <li><a href="#" class="icon brands fa-facebook-f"><span class="label">Facebook</span></a></li>
                    <li><a href="#" class="icon brands fa-github"><span class="label">GitHub</span></a></li>
                    <li><a href="#" class="icon brands fa-instagram"><span class="label">Instagram</span></a></li>
                    <li><a href="#" class="icon brands fa-linkedin-in"><span class="label">LinkedIn</span></a></li>
                  </ul>
                </li>
              </ul>
            </section>
          </div>
        </div>
      </section>

    <h1>{{ message }}</h1>
    <div v-for="cart in carts" v-bind:key="cart.id">
    <h2>{{cart.name}} {{ cart.id}}</h2>
    <h3>{{cart.location}}</h3>
    <img v-bind:src="cart.image_url" v-bind:alt="cart.name" style='width: 600px; height: 440px;' />
    <router-link v-bind:to="`/carts/${cart.id}/edit`">Edit Truck</router-link>
  </div>
  </div>
</template>

<style></style>
