<template>
  <div>
    <b-row>
      <data-table>
      </data-table>
    </b-row>
  </div>
</template>

<script>
import DataTable from "@/components/Dish/DataTable.vue";


export default {
  name: "HomeView",
  components: {
    DataTable,
  },
};
</script>
