<template>
  <div class="posts-index">
    <div class="card">
      <div
        v-for="post in posts"
        :key="post.id"
        v-bind:class="{ selected: post === currentPost }"
        v-on:click="currentPost = post"
      >
        <div class="card-body">
          <router-link v-bind:to="`/posts/${post.id}`">
            <h1>Title: {{ post.title }}</h1>
          </router-link>
          <p>Body: {{ post.body }}</p>
          <img v-bind:src="post.image" alt="post.title" />
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.selected {
  background-color: rgb(178, 247, 221);
  transition: 2s ease;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Here are posts",
      posts: [],
      currentPost: {},
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
