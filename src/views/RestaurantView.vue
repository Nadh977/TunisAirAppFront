<template>
  <div>
    <b-row>
      <data-table>
      </data-table>
    </b-row>
  </div>
</template>

<script>
import DataTable from "@/components/Restaurant/DataTable.vue";

export default {
  name: "RestaurantView",
  components: {
    DataTable,
  },
};
</script>