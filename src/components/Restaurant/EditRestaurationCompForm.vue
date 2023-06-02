<template>
  <b-form class="mt-3">
    <b-row>
      <b-row>
        <h4 class="text-secondary">Restauration Company Details</h4>
      </b-row>
      <b-col cols="12">
        <b-form-group id="name" label="Name" label-for="name">
          <b-form-input
              id="name"
              type="text"
              placeholder="Name"
              v-model="restcomp.name"
          ></b-form-input>
        </b-form-group>
      </b-col>
      <h4 class="text-secondary">Menus</h4>
    </b-row>
    <b-row class="mt-2">
      <li v-for="menu in menus" :key="menu.id" style="list-style-type: none;">
        <b-form-checkbox
            id="checked_menus"
            v-model="checkedMenus"
            :value="menu"
            name="checked_menus[]"
            unchecked-value=""
        >
          {{ menu.name }}
        </b-form-checkbox>
      </li>
    </b-row>

    <b-row class="mt-4">
      <b-col cols="3">
        <b-button variant="primary" class="px-5" @click="updateRestaurationComp"
        >Update Restauration Company</b-button
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
    restaurantId: Number,
  },
  data() {
    return {
      restcomp: {},
      menus: [],
      checkedMenus: [],
    };
  },
  mounted() {
    this.getRestaurationCompByID();
    this.getMenuData();
  },
  methods: {
    getMenuData() {
      axios
          .get("http://localhost:8090/api/foodmenu/foodmenus")
          .then((response) => {
            this.menus = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    triggerClose() {
      this.$emit("closeEditModal");
    },
    getRestaurationCompByID() {
      axios
          .get(`http://localhost:8090/api/restaurationcompany/${this.restaurantId}`)
          .then((response) => {
            this.restcomp = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    updateRestaurationComp() {
      this.restcomp.foodmenu = this.checkedMenus.map(menu => {
        const { id, name, dishes } = menu;
        return { id, name, dishes };
      });
      axios
          .put(
              `http://localhost:8090/api/restaurationcompany/modifyRestaurationcompanys/${this.restaurantId}`,
              this.restcomp
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