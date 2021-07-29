<template>
  <div class="posts-index">
    <div class="card">
      search by title
      <input v-model="titleFilter" />
      <div
        v-for="post in filterBy(posts, titleFilter, 'title', 'body')"
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
  background-color: rgb(229, 245, 236);
  transition: 2s ease;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  data: function () {
    return {
      message: "Here are posts",
      posts: [],
      currentPost: {},
      titleFilter: "",
    };
  },
  mixins: [Vue2Filters.mixin],
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
