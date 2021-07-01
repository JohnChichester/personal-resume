<template>
  <div class="login">
    <div class="col-lg-6 container-fluid">
      <div class="p-5">
        <div class="text-center">
          <h1>Login</h1>
        </div>
        <form class="user">
          <div class="form-group">
            <input
              type="email"
              class="form-control form-control-user"
              id="exampleInputEmail"
              aria-describedby="emailHelp"
              placeholder="Enter Email Address..."
            />
          </div>
          <div class="form-group">
            <input
              type="password"
              class="form-control form-control-user"
              id="exampleInputPassword"
              placeholder="Password"
            />
          </div>
          <div class="form-group">
            <div class="custom-control custom-checkbox small">
              <input type="checkbox" class="custom-control-input" id="customCheck" />
              <label class="custom-control-label" for="customCheck">Remember Me</label>
            </div>
          </div>
          <a href="/" class="btn btn-primary btn-user btn-block">Login</a>
        </form>
        <hr />

        <div class="text-center">
          <a class="small" href="Signup">Create an Account!</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      email: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          this.$parent.flashMessage = "Logged in successfully!";
          this.$router.push("/");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>
