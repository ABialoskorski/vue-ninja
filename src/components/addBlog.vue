<template>
  <div id="add-blog">
    <h1>Add a new Blog Post</h1>
    <form v-if="!submitted">
      <label>Blog Title:</label>
      <input type="text" v-model.lazy="blog.title" required>
      <label>Blog Content:</label>
      <textarea v-model.lazy="blog.content"></textarea>
      <div id="checkboxes">
        <input type="checkbox" value="Komputery" v-model="blog.categories">
        <label>Komputery</label>
        <input type="checkbox" value="Gry" v-model="blog.categories">
        <label>Gry</label>
        <input type="checkbox" value="Technologia" v-model="blog.categories">
        <label>Technologia</label>
        <input type="checkbox" value="Szachy" v-model="blog.categories">
        <label>Szachy</label>
      </div>
      <label>Author:</label>
      <select v-model="blog.author">
        <option v-for="(author,index) in authors" v-bind:key="index">{{author}}</option>
      </select>
      <p>
        <button v-on:click.prevent="post">Add Blog</button>
      </p>
    </form>
    <div v-if="submitted">
      <h2>Thanks for adding new post</h2>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog Title: {{blog.title}}</p>
      <p>Blog content:</p>
      <p>{{blog.content}}</p>
      <p>Blog Categories:</p>
      <ul>
        <li v-for="(category,index) in blog.categories" v-bind:key="index">{{category}}</li>
      </ul>
      <p>Author: {{blog.author}}</p>
    </div>
  </div>
</template>

<script>
// Imports

export default {
  components: {},
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: ""
      },
      authors: ["Artur", "Klaudia", "Pumpkin", "Pepper"],
      submitted: false
    };
  },
  methods: {
    post: function() {
      this.$http
        .post("https://blogs-vue-bd9f2.firebaseio.com/posts.json", this.blog)
        .then(function(data) {
          this.submitted = true;
        });
    }
  }
};
</script>

<style scoped>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 10px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h2 {
  color: green;
}
h3 {
  margin-top: 10px;
}
#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label {
  display: inline-block;
}
</style>