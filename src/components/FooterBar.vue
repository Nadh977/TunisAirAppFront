<template>
  <div class="footer-bar">
    <b-container>
      <b-row class="justify-content-between align-items-center">
        <b-col>
          <!-- Add any other content you may have in the footer here -->
        </b-col>
        <b-col class="text-right">
          <b-button class="logout-button" variant="danger" @click="logout">
            Logout
          </b-button>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<style scoped>
.footer-bar {
  background-color: #f8f9fa;
  padding: 10px;
}

.logout-button {
  color: white;
  background-color: red;
  border: none;
  border-radius: 4px;
  padding: 8px 16px;
  font-size: 14px;
  cursor: pointer;
  margin-left: 630px;
}

.logout-button:hover {
  opacity: 0.8;
}
</style>

<script>
export default {
  name: "FooterBar",
  methods: {
    logout() {
      // Perform logout logic here
      // Redirect to the login page
      this.$router.push("/");
    },
  },
};
</script>
