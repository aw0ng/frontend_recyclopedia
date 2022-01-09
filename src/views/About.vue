<template>
  <div class="about">
    <h1>Donors</h1>
    <div v-for="donor in donors" v-bind:key="donor.id">
      <h2>{{ donor.first_name }} {{ donor.last_name }}</h2>
      <h2>{{ donor.email }}</h2>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      donors: [],
    };
  },
  created: function () {
    this.indexDonors();
  },
  methods: {
    indexDonors: function () {
      axios.get("/api/donors").then((response) => {
        this.donors = response.data;
        console.log("donors index", response);
      });
    },
  },
};
</script>
