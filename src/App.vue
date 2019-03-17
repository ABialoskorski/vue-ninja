<template>
  <div>
    <blog-header></blog-header>
    <router-view></router-view>
  </div>
</template>

<script>
// Imports
import addBlog from "./components/addBlog.vue";
import showBlogs from "./components/showBlogs.vue";
import listBlogs from "./components/listBlogs.vue";
import blogHeader from "./components/blogHeader.vue";

export default {
  components: {
    "add-blog": addBlog,
    "show-blogs": showBlogs,
    "list-blogs": listBlogs,
    "blog-header": blogHeader
  },
  data() {
    return {};
  },
  methods: {}
};
</script>

<style scoped>
body {
  margin: 0;
  font-family: sans-serif;
}
</style>