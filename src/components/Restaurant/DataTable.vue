<template>
  <div>
    <b-row>
      <b-alert v-model="showSuccessAlert" variant="success" dismissible>
        {{ alertMessage }}
      </b-alert>
    </b-row>
    <b-row>
      <customer-overview
          :totalCustomers="numberOfCustomers"
          :activeCustomers="activeCustomers"
          @totalCustomersIsActive="setFilterTotalIsActive"
          @activeCustomerIsActive="setFilterActiveIsActive"
      ></customer-overview>
    </b-row>
    <b-row class="mt-3">
      <b-card>
        <b-row align-h="between">
          <b-col cols="6">
            <h3>{{ tableHeader }}</h3>
          </b-col>
          <b-col cols="2">
            <b-row>
              <b-col>
                <b-button
                    variant="primary"
                    id="show-btn"
                    @click="showCreateModal"
                >
                  <b-icon-plus class="text-white"></b-icon-plus>
                  <span class="h6 text-white">New Restauration Company</span>
                </b-button>
              </b-col>
            </b-row>
          </b-col>
        </b-row>
        <b-row class="mt-3">
          <b-table
              striped
              hover
              :items="items"
              :fields="fields"
              class="text-center"
          >
            <template #cell(contact_name)="data">
              {{
                `${data.item.name} `
              }}
            </template>
            <template #cell(foodmenu)="data">
              <ul>
                <li v-for="fm in data.item.foodmenu" :key="fm.id" style="list-style-type: none">{{ fm.name }}</li>
              </ul>
            </template>
            <template #cell(actions)="data">
              <b-row>
                <b-col cols="7">
                  <b-icon-pencil-square
                      class="action-item"
                      variant="primary"
                      @click="getRowData(data.item.id)"
                  ></b-icon-pencil-square>
                </b-col>
                <b-col cols="1">
                  <b-icon-trash-fill
                      class="action-item"
                      variant="danger"
                      @click="showDeleteModal(data.item.id)"
                  ></b-icon-trash-fill>
                </b-col>
              </b-row>
            </template>
          </b-table>
        </b-row>
      </b-card>
    </b-row>

    <!-- Modal for adding new customers -->
    <b-modal
        ref="create-customer-modal"
        size="xl"
        hide-footer
        title="New Restauration Company"
    >
      <create-customer-form
          @closeCreateModal="closeCreateModal"
          @reloadDataTable="getDishData"
          @showSuccessAlert="showAlertCreate"
      ></create-customer-form>
    </b-modal>

    <!-- Modal for updating customers -->
    <b-modal
        ref="edit-customer-modal"
        size="xl"
        hide-footer
        title="Edit Restauration Company"
    >
      <edit-customer-form
          @closeEditModal="closeEditModal"
          @reloadDataTable="getDishData"
          @showSuccessAlert="showAlertUpdate"
          :customerId="customerId"
      ></edit-customer-form>
    </b-modal>

    <!-- Delete Customer Modal -->
    <b-modal
        ref="delete-customer-modal"
        size="md"
        hide-footer
        title="Confirm Deletion"
    >
      <delete-customer-modal
          @closeDeleteModal="closeDeleteModal"
          @reloadDataTable="getDishData"
          @showDeleteAlert="showDeleteSuccessModal"
          :customerId="customerId"
      ></delete-customer-modal>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";
import CustomerOverview from "@/components/Restaurant/RestaurationCompOverview.vue";
import CreateCustomerForm from "@/components/Restaurant/CreateRestaurationCompForm.vue";
import EditCustomerForm from "@/components/Restaurant/EditRestaurationCompForm.vue";
import DeleteCustomerModal from "@/components/Restaurant/DeleteRestaurationCompModal.vue";

export default {
  components: {
    CustomerOverview,
    CreateCustomerForm,
    EditCustomerForm,
    DeleteCustomerModal,
  },
  data() {
    return {
      // Note 'isActive' is left out and will not appear in the rendered table

      fields: [

        {
          key: "name",
          label: "Name",
          sortable: false,
        },
        {
          key: "foodmenu",
          label: "Food menu",
          sortable: false,
        },
        "actions",
      ],
      items: [],
      numberOfCustomers: 0,
      activeCustomers: 0,
      activeCustomersData: [],
      customerId: 0,
      companySearchTerm: "",
      tableHeader: "",
      showSuccessAlert: false,
      alertMessage: "",
    };
  },
  mounted() {
    this.getDishData();
  },
  methods: {
    showCreateModal() {
      this.$refs["create-customer-modal"].show();
    },
    closeCreateModal() {
      this.$refs["create-customer-modal"].hide();
    },
    getDishData() {
      axios
          .get("http://localhost:8090/api/restaurationcompany/restaurationcompanys")
          .then((response) => {
            this.tableHeader = "Restauration Company";
            this.items = response.data;
            console.log(this.items);
            this.numberOfCustomers = response.data.length;
            this.activeCustomers = this.activeCustomersData.length;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    getRowData(id) {
      this.$refs["edit-customer-modal"].show();
      this.customerId = id;
    },
    closeEditModal() {
      this.$refs["edit-customer-modal"].hide();
    },
    setFilterTotalIsActive() {
      this.tableHeader = "Total Customers";
      this.getDishData();
    },
    setFilterActiveIsActive() {
      this.tableHeader = "Active Customers";
      this.items = this.activeCustomersData;
    },
    showAlertCreate() {
      this.showSuccessAlert = true;
      this.alertMessage = "Restauration Company was created successfully!";
    },
    showAlertUpdate() {
      this.showSuccessAlert = true;
      this.alertMessage = "Restauration Company was updated successfully";
    },
    showDeleteModal(id) {
      this.$refs["delete-customer-modal"].show();
      this.customerId = id;
    },
    closeDeleteModal() {
      this.$refs["delete-customer-modal"].hide();
    },
    showDeleteSuccessModal() {
      this.showSuccessAlert = true;
      this.alertMessage = "Restauration Company was deleted successfully!";
    },
  },
};
</script>

<style>
.action-item:hover {
  cursor: pointer;
}
</style>