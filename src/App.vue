<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="/">Website</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item active">
            <a class="nav-link" href="/">Home</a>
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/signup">Signup</a>
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/login">Login</a>
          </li>
          <li v-if="isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/logout">Logout</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/posts">Posts</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/posts/new">Create Post</a>
          </li>
        </ul>
      </div>
    </nav>

    <router-view />
  </div>
</template>
<style>
body {
  font-family: Rockwell Extra Bold, Rockwell Bold, monospace !important;
  background-image: url("./assets/ripples.png");
  text-align: center;
}
</style>
<script>
//import axios from "axios";

export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
