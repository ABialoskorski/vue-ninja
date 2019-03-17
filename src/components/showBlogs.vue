<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>All Blog articles</h1>
    <input type="text" v-model="search" placeholder="search blogs">
    <div v-for="(blog,index) in filteredBlogs" v-bind:key="index" class="single-blog">
      <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
      <article>{{blog.body | snippets}}</article>
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
      .get("http://jsonplaceholder.typicode.com/posts")
      .then(function(data) {
        this.blogs = data.body.slice(0, 10);
      });
  },
  computed: {},
  //Filters
  filters: {
    toUppercase(value) {
      return value.toUpperCase();
    }
  },
  directives: {
    rainbow: {
      bind(el, binding, vnode) {
        el.style.color =
          "#" +
          Math.random()
            .toString()
            .slice(2, 8);
      }
    }
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
</style>