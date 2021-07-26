<template>
  <div class="posts-index">
    <div class="card" v-for="post in posts" :key="post.id">
      <div class="card-body">
        <h1>Title: {{ post.title }}</h1>
        <p>Body: {{ post.body }}</p>
        <img v-bind:src="post.image" alt="post.title" />
      </div>
    </div>
    <h1>{{ message }}</h1>
    <div v-for="post in posts" :key="post.id">
      <router-link v-bind:to="`/posts/${post.id}`">
        <h2>Title: {{ post.title }}</h2>
      </router-link>
      <p>Content: {{ post.body }}</p>
      <img v-bind:src="post.image" alt="post.title" />
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Here are posts",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        this.posts = response.data;
        console.log("All Posts:", this.posts);
      });
    },
  },
};
</script>
