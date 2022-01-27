<template>
  <div class="Profile">
    <h1>Profile</h1>
    <div>
      <h2>{{ donor.first_name }} {{ donor.last_name }}</h2>
      <h2>{{ donor.email }}</h2>
      <div class="row justify-content-center">
        <div class="col-lg-8">
          <img class="img-cover" v-bind:src="donor.image" v-bind:alt="donor.first_name" />
        </div>
      </div>
    </div>
    <h1>My Items</h1>
    <div v-for="item in items" v-bind:key="item.id">
      <h2>{{ item.item }}</h2>
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
      donor: {},
      items: [],
    };
  },
  created: function () {
    this.showDonor();
    this.donorItems();
  },
  methods: {
    showDonor: function () {
      axios.get("/api/donors/" + this.$route.params.id).then((response) => {
        console.log("donor show", response);
        this.donor = response.data;
      });
    },
    donorItems: function () {
      axios.get("/api/items").then((response) => {
        this.items = response.data;
        console.log("items index", response);
      });
    },
  },
};
</script>
