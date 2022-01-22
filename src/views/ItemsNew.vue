<template>
  <div class="items-new">
    <h1>New Item</h1>
    <form v-on:submit.prevent="createItem()">
      <ul>
        <li v-for="error in errors" v-bind:key="error.id">{{ error }}</li>
      </ul>
      Item:
      <input type="text" v-model="newItemName" />
      Condition:
      <input type="text" v-model="newItemCondition" />
      Quantity:
      <input type="text" v-model="newItemQuantity" />
      Category:
      <input type="text" v-model="newItemCategory" />
      Image:
      <input type="text" v-model="newItemImage" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newItemName: "",
      newItemCondition: "",
      newItemQuantity: "",
      newItemCategory: "",
      newItemImage: "",
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createItem: function () {
      var params = {
        name: this.newItemName,
        condition: this.newItemCondition,
        quantity: this.newItemQuantity,
        category: this.newItemCategory,
        image: this.newItemImage,
      };
      axios
        .post("/api/items", params)
        .then((response) => {
          console.log("items create", response);
          this.$router.push("/items");
        })
        .catch((error) => {
          console.log("items create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
