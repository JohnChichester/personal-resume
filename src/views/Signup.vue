<template>
  <div class="container-fluid">
    <div class="signup card bg-gradient-light shadow mb-4">
      <form v-on:submit.prevent="submit()">
        <div class="card-header bg-dark py-3">
          <h6 class="m-0 font-weight-bold text-white">Signup</h6>
        </div>
        <div class="container-fluid">
          <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
          </ul>
          <div>
            <label>First Name:</label>
            <input type="text" v-model="first_name" />
          </div>
          <div>
            <label>Last Name:</label>
            <input type="text" v-model="last_name" />
          </div>
          <div>
            <label>Email:</label>
            <input type="email" v-model="email" />
            <br />
            <small v-if="email.length == 6">+ 9 = Fuggin Nice</small>
          </div>
          <div>
            <label>Password:</label>
            <input type="password" v-model="password_digest" />
            <br />
            <small v-if="password_digest.length > 0 && password_digest.length < 6" class="text-danger">
              Password MUST be atleast 6 characters!
            </small>
          </div>
          <div>
            <label>Password confirmation:</label>
            <input type="password" v-model="password_confirmation" />
            <br />
            <small v-if="password != passwordConfirmation" class="text-danger">Passwords must match!</small>
          </div>
          <div>
            <label>Phone Number:</label>
            <input type="text" v-model="phone_number" />
            <br />
            <small v-if="phone_number.length > 7 && phone_number.length < 10" class="text-danger">
              Phone number must be atleast 10 digits!
            </small>
          </div>
          <div>
            <label>Bio: (Give us a brief summary of yourself!)</label>
            <input type="text" v-model="bio" />
          </div>
          <div>
            <label>LinkedIn URL:</label>
            <input type="url" v-model="linkedin" />
          </div>
          <div>
            <label>Twitter Handle:</label>
            <input type="text" v-model="twitter_handle" />
          </div>
          <div>
            <label>Personal Website URL:</label>
            <input type="url" v-model="website" />
          </div>
          <div>
            <label>Resume URL:</label>
            <input type="url" v-model="resume_url" />
          </div>
          <div>
            <label>GitHub:</label>
            <input type="url" v-model="github" />
          </div>
          <div>
            <label>Photo:</label>
            <input type="string" v-model="photo" />
            <div class="text-grey-30 small">Show us that smile!</div>
          </div>
          <a href="#" class="btn btn-info btn-icon-split">
            <span class="icon text-white-50">
              <i class="fas fa-arrow-right"></i>
            </span>
            <input class="bg-info" type="submit" value="Submit" />
          </a>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      first_name: "",
      last_name: "",
      email: "",
      password_digest: "",
      password_confirmation: "",
      phone_number: "",
      bio: "",
      linkedin: "",
      twitter_handle: "",
      website: "",
      resume_url: "",
      github: "",
      photo: "",
      errors: [],
      status: null,
    };
  },
  methods: {
    submit: function () {
      var params = {
        first_name: this.first_name,
        last_name: this.last_name,
        email: this.email,
        password_digest: this.password_digest,
        password_confirmation: this.password_confirmation,
        phone_number: this.phone_number,
        bio: this.bio,
        linkedin: this.linkedin,
        twitter_handle: this.twitter_handle,
        website: this.website,
        resume_url: this.resume_url,
        github: this.github,
        photo: this.photo,
      };
      axios
        .post("/students", params)
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
