<template>
  <b-form class="mt-3">
    <b-row>
      <b-row>
        <h4 class="text-secondary">Dish Details</h4>
      </b-row>
      <b-col cols="6">
        <b-form-group id="dish-name" label="Name of the Dish" label-for="dish-name">
          <b-form-input
              id="dish-name"
              type="text"
              placeholder="Name of the Dish"
              v-model="dish.name"
          ></b-form-input>
        </b-form-group>
      </b-col>
      <b-col cols="6">
        <b-form-group id="description" label="Description" label-for="description">
          <b-form-input
              id="description"
              type="text"
              placeholder="Description"
              v-model="dish.description"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-3">
      <b-col cols="6">
        <b-form-group id="price" label="Price" label-for="price">
          <b-form-input
              id="price"
              type="number"
              placeholder="price"
              v-model="dish.price"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-4">
      <b-col cols="3">
        <b-button variant="primary" class="px-5" @click="addNewDish"
        >Add Dish</b-button
        >
      </b-col>
      <b-col>
        <b-button variant="warning" @click="triggerClose">Close</b-button>
      </b-col>
    </b-row>
  </b-form>
</template>

<script>
import axios from "axios";

export default {
  name: "CreateDishModal",
  data() {
    return {
      dish: {},
    };
  },
  methods: {
    triggerClose() {
      this.$emit("closeCreateModal");
    },
    addNewDish() {
      axios
          .post("http://localhost:8090/api/dish/create", this.dish)
          .then((response) => {
            console.log(response.data);
            this.$emit("closeCreateModal");
            this.$emit("reloadDataTable");
            this.$emit("showSuccessAlert");
          })
          .catch((error) => {
            console.log(error);
          });
    },
  },
};
</script>