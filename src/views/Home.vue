<template>
  <div class="home">
    <h1>ALL ITEMS</h1>
    <div v-for="item in items" v-bind:key="item.id">
      <h2>{{ item.item }}</h2>
      <p>Quantity: {{ item.quantity }}</p>
      <p>Condition: {{ item.condition }}</p>
      <div class="row justify-content-center">
        <div class="col-lg-8">
          <img class="img-cover" v-bind:src="item.image" v-bind:alt="item.item" />
        </div>
      </div>
    </div>
    <h1>CATEGORIES</h1>
    <div v-for="category in categories" v-bind:key="category.category_type">
      <h2>{{ category.category_type }}</h2>
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
      items: [],
      categories: [],
    };
  },
  created: function () {
    this.indexItems();
    this.indexCategories();
  },
  methods: {
    indexItems: function () {
      axios.get("/api/items").then((response) => {
        this.items = response.data;
        console.log("items index", response);
      });
    },
    indexCategories: function () {
      axios.get("/api/categories").then((response) => {
        this.categories = response.data;
        console.log("categories index", response);
      });
    },
  },
};
</script>
