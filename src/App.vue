<template>
  <div id="app">
    <!--Topbar -->
    <nav class="navbar navbar-expand navbar-light bg-gradient-light topbar mb-4 static-top shadow">
      <!-- Sidebar Toggle (Topbar) -->

      <!-- Topbar Search -->
      <div class="nav-item">
        <a class="nav-link card bg-dark text-white shadow" href="/">
          <div class="card-body">Home</div>
        </a>
      </div>
      <div class="nav-item" v-if="!isLoggedIn()">
        <a class="nav-link card bg-secondary text-white shadow" href="/Login">
          <div class="card-body">Login</div>
        </a>
      </div>
      <div class="nav-item" v-if="!isLoggedIn()">
        <a class="nav-link card bg-dark text-white shadow" href="/Signup">
          <div class="card-body">Signup</div>
        </a>
      </div>
      <div class="nav-item" v-if="isLoggedIn()">
        <a class="nav-link card bg-secondary text-white shadow" href="/Logout">
          <div class="card-body">Logout</div>
        </a>
      </div>
      <!--<form
        class="d-none d-sm-inline-block form-inline mr-auto ml-md-3 my-2 my-md-0 mw-100 position:right navbar-search"
      >
        <div class="input-group">
          <input
            type="text"
            class="form-control bg-light border-0 small"
            placeholder="Search for..."
            aria-label="Search"
            aria-describedby="basic-addon2"
          />
          <div class="input-group-append">
            <button class="btn btn-primary" type="button">
              <i class="fas fa-search fa-sm"></i>
            </button>
          </div>
        </div>
      </form>-->
      <!-- Topbar Navbar -->
      <ul class="navbar-nav ml-auto">
        <!-- Nav Item - Search Dropdown (Visible Only XS) -->
        <li class="nav-item dropdown no-arrow d-sm-none">
          <a
            class="nav-link dropdown-toggle"
            href="#"
            id="searchDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <i class="fas fa-search fa-fw"></i>
          </a>
          <!-- Dropdown - Messages -->
          <div class="dropdown-menu dropdown-menu-right p-3 shadow animated--grow-in" aria-labelledby="searchDropdown">
            <form class="form-inline mr-auto w-100 navbar-search">
              <div class="input-group">
                <input
                  type="text"
                  class="form-control bg-light border-0 small"
                  placeholder="Search for..."
                  aria-label="Search"
                  aria-describedby="basic-addon2"
                />
                <div class="input-group-append">
                  <button class="btn btn-primary" type="button">
                    <i class="fas fa-search fa-sm"></i>
                  </button>
                </div>
              </div>
            </form>
          </div>
        </li>
        <!-- Nav Item - User Information -->
        <li class="nav-item dropdown no-arrow">
          <a
            class="nav-link dropdown-toggle"
            href="#"
            id="userDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <span class="mr-2 d-none d-lg-inline text-gray-600 small">
              {{ student.first_name + " " + student.last_name }}
            </span>
            <img class="img-profile rounded-circle" src="img/undraw_profile.svg" />
          </a>
          <!-- Dropdown - User Information -->
          <div class="dropdown-menu dropdown-menu-right shadow animated--grow-in" aria-labelledby="userDropdown">
            <a class="dropdown-item" href="#">
              <i class="fas fa-user fa-sm fa-fw mr-2 text-gray-400"></i>
              Profile
            </a>
            <a class="dropdown-item" href="#">
              <i class="fas fa-cogs fa-sm fa-fw mr-2 text-gray-400"></i>
              Settings
            </a>
            <a class="dropdown-item" href="#">
              <i class="fas fa-list fa-sm fa-fw mr-2 text-gray-400"></i>
              Activity Log
            </a>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="#" data-toggle="modal" data-target="#logoutModal">
              <i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>
              Logout
            </a>
          </div>
        </li>
      </ul>
    </nav>
    <div v-if="flashMessage" v-on:click="flashMessage = null" class="alert alert-success" role="alert">
      {{ flashMessage }}
    </div>
    <!-- End of Topbar -->
    <router-view />
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      student: {},
      flashMessage: null,
    };
  },
  created: function () {
    this.showStudents();
  },

  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    showStudents: function () {
      axios.get("/students/1").then((response) => {
        console.log("show student profile", response.data);
        this.student = response.data;
      });
    },
  },
};
</script>
