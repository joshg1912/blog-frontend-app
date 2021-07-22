<template>
  <div class="post-show">
    <div>
      <h1>{{ post.title }}</h1>
      <p>{{ post.body }}</p>
      <p>{{ post.image }}</p>
      <router-link to="/posts">Back to Posts</router-link>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/1").then((response) => {
      this.post = response.data;
    });
  },
};
</script>
