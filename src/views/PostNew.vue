<template>
  <div class="posts-new">
    <img v-if="status" :src="`https://http.cat/[status_code]`" />
    <form v-on:submit.prevent="createPost()">
      <h1>Create Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <small v-if="newPostParams.body.length > 500" class="text-danger">cannot exceed 500 characters</small>
        <small>{{ 500 - newPostParams.body.length }} characters remaining</small>
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      newPostParams: { body: "" },
      status: "",
    };
  },
  methods: {
    createPost: function () {
      console.log("Creating Post");
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          this.$router.push("/posts");
          console.log(response.data);
        })
        .catch((error) => {
          this.status = error.response.status;
        });
    },
  },
};
</script>
