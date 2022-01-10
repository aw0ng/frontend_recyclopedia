<template>
  <div class="about">
    <h1>Donors</h1>
    <div v-for="donor in donors" v-bind:key="donor.id">
      <h2>{{ donor.first_name }} {{ donor.last_name }}</h2>
      <h2>{{ donor.email }}</h2>
      <div class="row justify-content-center">
        <div class="col-lg-8">
          <img class="img-cover" v-bind:src="donor.image" v-bind:alt="donor.first_name" />
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.img-cover {
  height: 250px;
  width: 40%;
  object-fit: cover;
}
</style>

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
