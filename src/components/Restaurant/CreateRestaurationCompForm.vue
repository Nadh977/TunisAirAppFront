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
        <b-button variant="primary" class="px-5" @click="addNewRestComp">Add Menu</b-button>
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
      restcomp: {},
      menus: [],
      checkedMenus: [],
    };
  },
  mounted() {
    this.getMenuData();
  },
  methods: {
    triggerClose() {
      this.$emit("closeCreateModal");
    },
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
    addNewRestComp() {
      // Set the selected dish details to the menu object
      this.restcomp.foodmenu = this.checkedMenus.map(menu => {
        const { id, name, dishes } = menu;
        return { id, name, dishes };
      });

      // Send the updated menu object to the backend
      axios
          .post("http://localhost:8090/api/restaurationcompany/create", this.restcomp)
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
