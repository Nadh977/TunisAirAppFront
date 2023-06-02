<template>
  <b-form class="mt-3">
    <b-row>
      <b-row>
        <h4 class="text-secondary">Menu Details</h4>
      </b-row>
      <b-col cols="12">
        <b-form-group id="name" label="Name" label-for="name">
          <b-form-input
              id="name"
              type="text"
              placeholder="Name"
              v-model="menu.name"
          ></b-form-input>
        </b-form-group>
      </b-col>
      <h4 class="text-secondary">Dishes</h4>
    </b-row>
    <b-row class="mt-1">
      <li v-for="dish in dishes" :key="dish.id" style="list-style-type: none;">
        <b-form-checkbox
            id="selected_dishes"
            v-model="checkedDishes"
            :value="dish"
            name="selected_dishes[]"
            unchecked-value=""
        >
          {{ dish.name }}
        </b-form-checkbox>
      </li>
    </b-row>
    <b-row class="mt-4">
      <b-col cols="3">
        <b-button variant="primary" class="px-5" @click="addNewMenu">Add Menu</b-button>
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
  name: "CreateMenuModal",
  data() {
    return {
      menu: {},
      dishes: [],
      checkedDishes: [],
    };
  },
  mounted() {
    this.getDishData();
  },
  methods: {
    triggerClose() {
      this.$emit("closeCreateModal");
    },
    getDishData() {
      axios
          .get("http://localhost:8090/api/dish/dishes")
          .then((response) => {
            this.dishes = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    addNewMenu() {
      // Set the selected dish details to the menu object
      this.menu.dishes = this.checkedDishes.map(dish => {
        const { id, name, description, price } = dish;
        return { id, name, description, price };
      });

      // Send the updated menu object to the backend
      axios
          .post("http://localhost:8090/api/foodmenu/create", this.menu)
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
