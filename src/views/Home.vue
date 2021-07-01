<template>
  <div>
    <h1>Here is your profile:</h1>
    <h2>{{ student }}</h2>
    <form @submit.prevent="submit">
      <input type="text" v-model="experiences" />
      <button type="submit" v-on:click="saveExperience()">Add an experience</button>
    </form>
    <div class="container-fluid">
      <div class="card mb-4">
        <div class="card-header">
          <h1>{{ student.first_name + " " + student.last_name }}</h1>
          <div class="text-primary-50 med">{{ student.email }}</div>
        </div>
        <div class="card-body">
          {{ student.bio }}
        </div>
      </div>
      <div class="row">
        <div class="col-xl-3 col-md-6 mb-4">
          <div class="card border-left-success shadow h-100 py-2">
            <div class="card-body">
              <div class="row no-gutters align-items-center">
                <div class="col mr-2">
                  <div class="text-xs font-weight-bold text-success text-uppercase mb-1">Phone Number</div>
                  <div class="h5 mb-0 font-weight-bold text-gray-800">{{ student.phone_number }}</div>
                </div>
                <div class="col-auto">
                  <i class="fas fa-phone fa-2x text-gray-300"></i>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-xl-3 col-md-6 mb-4">
          <div class="card border-left-warning shadow h-100 py-2">
            <div class="card-body">
              <div class="row no-gutters align-items-center">
                <div class="col mr-2">
                  <div class="text-xs font-weight-bold text-warning text-uppercase mb-1">Website</div>
                  <div class="h5 mb-0 font-weight-bold text-gray-800">{{ student.website }}</div>
                </div>
                <div class="col-auto"></div>
                <i class="fas fa-mouse fa-2x text-gray-300"></i>
              </div>
            </div>
          </div>
        </div>
        <div class="col-xl-3 col-md-6 mb-4">
          <div class="card border-left-primary shadow h-100 py-2">
            <div class="card-body">
              <div class="row no-gutters align-items-center">
                <div class="col mr-2">
                  <div class="text-xs font-weight-bold text-primary text-uppercase mb-1">Twitter Handle</div>
                  <div class="h5 mb-0 font-weight-bold text-gray-800">{{ student.twitter_handle }}</div>
                </div>
                <div class="col-auto">
                  <i class="fas fa-bird fa-2x text-gray-300"></i>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-xl-3 col-md-6 mb-4">
          <div class="card border-left-danger shadow h-100 py-2">
            <div class="card-body">
              <div class="row no-gutters align-items-center">
                <div class="col mr-2">
                  <div class="text-xs font-weight-bold text-danger text-uppercase mb-1">GitHub</div>
                  <div class="h5 mb-0 font-weight-bold text-gray-800">{{ student.github }}</div>
                </div>
                <div class="col-auto">
                  <i class="fas fa-hack fa-2x text-gray-300"></i>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      student: {},
      experiences: [],
    };
  },
  created: function () {
    this.showStudents();
  },
  methods: {
    showStudents: function () {
      axios.get("/students/1").then((response) => {
        console.log("show student profile", response.data);
        this.student = response.data;
      });
    },
    destroyStudents: function () {
      console.log("destroy profile", this.student);
      axios.delete("/students/" + this.student.id).then((response) => {
        console.log("Destroy success", response.data);
        this.$router.push("/");
      });
    },
    saveExperience: function () {
      this.experiences.push();
    },
    showExperiences: function () {
      console.log(this.experiences);
    },
  },
};
</script>
