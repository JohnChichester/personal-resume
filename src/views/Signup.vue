<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="name" />
        <br />
        <small>Username has {{ 20 - name.length }} characters remaining.</small>
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="email" />
        <br />
        <small v-if="email.length == 6">+ 9 = Fuggin Nice</small>
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="password" />
        <br />
        <small v-if="password.length > 0 && password.length < 6" class="text-danger">
          Password MUST be atleast 6 characters!
        </small>
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="passwordConfirmation" />
        <br />
        <small v-if="password != passwordConfirmation" class="text-danger">Passwords must match!</small>
      </div>
      <div>
        <label>Phone Number</label>
        <input type="text" v-model="phone_number" />
        <br />
        <small v-if="phone_number.length < 10" class="text-danger">Phone number must be atleast 10 digits!</small>
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      phone_number: "",
      errors: [],
      status: null,
    };
  },
  methods: {
    submit: function () {
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/users", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>
