<template>
  <div class="home">
    <h1>New Place</h1>
    <div>
      Name: <input type="text" v-model="newPlaceName" /> Address: <input type="text" v-model="newPlaceAddress" />
      <button v-on:click="createPlace()">Create Place</button>
    </div>
    <h1>All Places</h1>
    <div v-for="place in places">
      <h2>{{ place.name }}</h2>
      <!-- <img v-bind:src="place.url" /> -->
      <p>Name: {{ place.name }}</p>
      <p>Address: {{ place.address }}</p>
    </div>
    <!--  <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  data: function() {
    return {
      places: [],
      newPlaceName: "",
      newPlaceAddress: ""
    };
  },
  created: function() {
    axios.get("/api/places").then(response => {
      this.places = response.data;
    });
  },
  methods: {
    createPlace: function() {
      var params = {
        name: this.newPlaceName,
        address: this.newPlaceAddress
      };
      axios.post("/api/places", params).then(response => {
        this.places.push(response.data);
        this.newPlaceName = "";
        this.newPlaceAddress = "";
      });
    }
  }
};
</script>
