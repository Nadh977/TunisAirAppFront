<template>
  <b-navbar toggleable="lg" type="light" variant="primary" class="custom-navbar">
    <b-container>
      <b-row class="align-items-center">
        <b-col>
          <img :src="MyImage" alt="My Image" style="margin-right: 10px;"/>
          <span class="h3 text-black-50">Tunisair Food</span>
        </b-col>
        <b-col class="ml-auto">
          <b-navbar-nav>
            <b-nav-item to="/home" exact active-class="active-link" class="nav-link">Dishes</b-nav-item>
            <b-nav-item to="/menu" active-class="active-link" class="nav-link">Menus</b-nav-item>
            <b-nav-item to="/restaurant" active-class="active-link" class="nav-link">Restaurants</b-nav-item>
            <b-nav-item to="/" active-class="active-link" class="nav-link" style="position: absolute; right: 0; ">Logout</b-nav-item>
          </b-navbar-nav>
        </b-col>
      </b-row>
    </b-container>
  </b-navbar>
</template>

<style scoped>
.active-link {

  color: #ffffff !important;
}
.custom-navbar {
  background-color: #ef9999 !important;; /* Replace with your desired shade of red */
}

</style>

<script>
import MyImage from '@/assets/travelling.png';
export default {
  data() {
    return {
      MyImage: MyImage,
    };
  },
  name: "HeaderBar",
};
</script>
