<template>
  <div>
    <h1>Here is your profile:</h1>
    <h2>{{ student }}</h2>
    <form @submit.prevent="submit">
      <input type="text" v-model="experiences" />
      <button type="submit" v-on:click="saveExperience()">Add an experience</button>
    </form>
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
