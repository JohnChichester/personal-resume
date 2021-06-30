<template>
  <div>
    <h1>Here is your profile:</h1>
    <h2>{{ student }}</h2>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      student: {},
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
      console.log("destroy profile", this.post);
      axios.delete("/students/" + this.post.id).then((response) => {
        console.log("Destroy success", response.data);
        this.$router.push("/");
      });
    },
  },
};
</script>
