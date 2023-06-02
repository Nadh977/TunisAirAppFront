<template>
  <div class="container">
    <div class="main" >
      <h1>Join us !</h1>
      <form @submit="sendCredentials">
        <div class="input-container">
          <input
              type="text"
              name="username"
              id="username"
              placeholder="User Name"
              v-model="username"
          />
          <input
              type="password"
              name="password"
              id="password"
              placeholder="password"
              v-model="password"
          />
        </div>
        <button class="button" id="done" type="submit">Done!</button>
      </form>
      <p>Already have an account? <router-link to="/">Log in here!</router-link></p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "LoginView",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    sendCredentials(event) {
      event.preventDefault(); // Prevent form submission

      const data = {
        username: this.username,
        password: this.password,
      };

      axios
          .post("http://localhost:8090/api/auth/register", data)
          .then((response) => {
            // Handle success response
            console.log(response);

            // Redirect to the "/" page
            this.$router.push("/home");
          })
          .catch((error) => {
            // Handle error
            console.error(error);
          });
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.main {
  background: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
  width: 450px;
  text-align: center;
  border-radius: 1.5rem;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  padding: 30px;
  font-family: "Poppins", sans-serif;
}

h1 {
  color: #fff;
  font-size: 24px;
  font-weight: 500;
  margin-bottom: 20px;
}

.input-container {
  display: block;
  flex-direction: column;
  align-items: center;
  margin-bottom: 15px;
}

input {
  background-color: rgba(255, 255, 255, 0.6);
  border-radius: 2rem;
  border: none;
  padding: 15px;
  text-align: center;
  outline: none;
  margin-bottom: 15px;
  width: 80%;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
  font-weight: 400;
  transition: background-color 0.3s ease;
}

input:hover {
  background-color: rgba(255, 255, 255, 0.8);
}

input:focus {
  background-color: #fff;
}

#done {
  background: #5cb85c;
  color: #fff;
  border-radius: 2rem;
  border: none;
  padding: 15px 40px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  outline: none;
  transition: background-color 0.3s ease;
  margin-bottom: 15px;
}

#done:hover {
  background-color: #4cae4c;
}

.button {
  cursor: pointer;
}
</style>
