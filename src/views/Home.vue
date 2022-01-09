<template>
  <div class="home">
    <h1>ALL items</h1>
    <div v-for="item in items" v-bind:key="item.id">
      <h2>{{ item.item }}</h2>
      <p>Quantity: {{ item.quantity }}</p>
      <p>Condition: {{ item.condition }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      items: [],
    };
  },
  created: function () {
    this.indexItems();
  },
  methods: {
    indexItems: function () {
      axios.get("/api/items").then((response) => {
        this.items = response.data;
        console.log("items index", response);
      });
    },
  },
};
</script>
