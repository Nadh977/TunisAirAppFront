<template>
  <div>
    <header-bar v-if="shouldShowHeaderBar"></header-bar>
    <b-container>
      <b-row className="mt-5">
        <router-view/>
      </b-row>
    </b-container>
    <footer-bar v-if="shouldShowFooterBar"></footer-bar>
  </div>
</template>

<script>
import HeaderBar from "@/components/HeaderBar.vue";
import FooterBar from "@/components/FooterBar.vue";

export default {
  components: {
    HeaderBar,
    FooterBar,
  },
  computed: {
    shouldShowHeaderBar() {
      // Get the current route name
      const currentRoute = this.$route.name;

      // Determine if the header bar should be shown based on the current route
      return !["login", "signup"].includes(currentRoute);
    },
    shouldShowFooterBar() {
      // Get the current route name
      const currentRoute = this.$route.name;

      // Determine if the footer bar should be shown based on the current route
      return !["login", "signup"].includes(currentRoute);
    },
  },
};
</script>
