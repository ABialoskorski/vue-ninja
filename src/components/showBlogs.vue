<template>
  <div id="show-blogs">
    <h1>All Blog articles</h1>
    <input type="text" v-model="search" placeholder="search blogs">
    <div v-for="(blog,index) in filteredBlogs" v-bind:key="index" class="single-blog">
      <router-link v-bind:to="'/blog/' + blog.id">
        <h2>{{blog.title}}</h2>
      </router-link>
      <article>{{blog.content}}</article>
    </div>
  </div>
</template>

<script>
import searchMixin from "../mixins/searchMixin";

export default {
  components: {},
  data() {
    return {
      blogs: [],
      search: ""
    };
  },
  methods: {},
  created() {
    this.$http
      .get("https://blogs-vue-bd9f2.firebaseio.com/posts.json")
      .then(function(data) {
        return data.json();
      })
      .then(function(data) {
        var blogsArray = [];
        for (let key in data) {
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      });
  },
  mixins: [searchMixin]
};
</script>

<style scoped>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
a {
  color: black;
  text-decoration: none;
}
</style>