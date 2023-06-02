<template>
  <div>
    <b-row>
      <data-table>
      </data-table>
    </b-row>
  </div>
</template>

<script>
import DataTable from "@/components/Menu/DataTable.vue";

export default {
  name: "MenuView",
  components: {
    DataTable,
  },
};
</script>