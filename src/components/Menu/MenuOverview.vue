<template>
  <div>
    <b-row class="text-center">
      <b-col>
        <div
            style="color: #b02828"
            class="filter-card p-3"

            @click="totalCustomersIsActiveFilter"
        >
          <h6>Total Menus</h6>
          <h4>
            <strong>{{ totalCustomers }}</strong>
          </h4>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "MenuOverview",
  props: {
    totalCustomers: Number,
    activeCustomers: Number,
  },
  data() {
    return {
      totalIsActive: true,
      activeIsActive: false,
    };
  },
  methods: {
    totalCustomersIsActiveFilter() {
      this.totalIsActive = true;
      this.activeIsActive = false;
      this.$emit("totalCustomersIsActive");
    },
  },
};
</script>

<style>
.filter-card:hover {
  cursor: pointer;
  text-decoration: underline;
}

.bg-active-filter {
  background-color: #e9f1fe;
  color: #074297;
}
</style>