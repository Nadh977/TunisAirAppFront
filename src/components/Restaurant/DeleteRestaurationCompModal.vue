<template>
  <div>
    <b-row class="mt-2 mb-3">
      <h6 class="text-secondary">
        Are you sure you want to delete this Restauration Company from your CRM?
      </h6>
    </b-row>
    <b-row class="mt-2 mb-3">
      <p class="text-danger">
        This action is not reversible and may result in the loss if important
        data.
      </p>
    </b-row>
    <b-row class="mt-4">
      <b-col>
        <b-button variant="danger" @click="removeRestCompFromData"
        >Delete Restauration Company</b-button
        >
      </b-col>
      <b-col>
        <b-button variant="warning" @click="triggerClose">Close</b-button>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "DeleteCustomerModal",
  props: {
    restaurantId: Number,
  },
  methods: {
    triggerClose() {
      this.$emit("closeDeleteModal");
    },
    removeRestCompFromData() {
      axios
          .delete(`http://localhost:8090/api/restaurationcompany/deleteRestaurationCompany/${this.restaurantId}`)
          .then(() => {
            this.$emit("reloadDataTable");
            this.$emit("showDeleteAlert");
            this.$emit("closeDeleteModal");
          })
          .catch((error) => {
            console.log(error);
          });
    },
  },
};
</script>