<template>
  <b-form class="mt-3">
    <b-row>
      <b-row>
        <h4 class="text-secondary">Dish Details</h4>
      </b-row>
      <b-col cols="6">
        <b-form-group id="first-name" label="Name" label-for="first-name">
          <b-form-input
              id="first-name"
              type="text"
              placeholder="name"
              v-model="customer.name"
          ></b-form-input>
        </b-form-group>
      </b-col>
      <b-col cols="6">
        <b-form-group id="last-name" label="Description" label-for="last-name">
          <b-form-input
              id="last-name"
              type="text"
              placeholder="description"
              v-model="customer.description"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-3">
      <b-col cols="6">
        <b-form-group id="email" label="Price" label-for="email">
          <b-form-input
              id="email"
              type="number"
              placeholder="price"
              v-model="customer.price"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>

    <b-row class="mt-4">
      <b-col cols="3">
        <b-button variant="primary" class="px-5" @click="updateDish"
        >Update Dish</b-button
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
  name: "CreateCustomerModal",
  props: {
    dishId: Number,
  },
  data() {
    return {
      customer: {},
    };
  },
  mounted() {
    this.getDishByID();
  },
  methods: {
    triggerClose() {
      this.$emit("closeEditModal");
    },
    getDishByID() {
      axios
          .get(`http://localhost:8090/api/dish/${this.dishId}`)
          .then((response) => {
            this.customer = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    updateDish() {
      axios
          .put(
              `http://localhost:8090/api/dish/modifyDish/${this.dishId}`,
              this.customer
          )
          .then((response) => {
            console.log(response.data);
            this.$emit("closeEditModal");
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