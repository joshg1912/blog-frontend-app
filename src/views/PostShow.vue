<template>
  <div class="post-show">
    <div>
      <h1>Title: {{ post.title }}</h1>
      <p>Body: {{ post.body }}</p>
      <router-link v-bind:to="`/posts/${post.id}/edit`"><button>Edit Post</button></router-link>
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
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
    });
  },
};
</script>
