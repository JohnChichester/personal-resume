<template>
  <div>
    <div class="card mb-4">
      <div class="card-header">
        <h1>{{ student.first_name + " " + student.last_name }}</h1>
      </div>
      <div class="card-body">
        This card uses Bootstrap's default styling with no utility classes added. Global styles are the only things
        modifying the look and feel of this default card example.
      </div>
    </div>

    <!-- Basic Card Example -->
    <div class="card shadow mb-4">
      <div class="card-header py-3">
        <h6 class="m-0 font-weight-bold text-primary">Basic Card Example</h6>
      </div>
      <div class="card-body">
        The styling for this basic card example is created by using default Bootstrap utility classes. By using utility
        classes, the style of the card component can be easily modified with no need for any custom CSS!
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
