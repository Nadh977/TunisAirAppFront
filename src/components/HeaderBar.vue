<template>
  <b-navbar toggleable="lg" type="dark" variant="primary">
    <b-container>
      <b-row class="align-items-center">
        <b-col>
          <b-icon-people-fill class="h2 text-white"></b-icon-people-fill>
          <span class="h3 text-white">CRM</span>
        </b-col>
        <b-col class="ml-auto">
          <b-navbar-nav>
            <b-nav-item to="/home" exact active-class="active-link" class="nav-link">Dishes</b-nav-item>
            <b-nav-item to="/menu" active-class="active-link" class="nav-link">Menus</b-nav-item>
            <b-nav-item to="/restaurant" active-class="active-link" class="nav-link">Restaurants</b-nav-item>
          </b-navbar-nav>
        </b-col>
      </b-row>
    </b-container>
  </b-navbar>
</template>

<style>
.active-link {
  background-color: #0465e3;
  color: #ffffff !important;
}

</style>

<script>
export default {
  name: "HeaderBar",
};
</script>
