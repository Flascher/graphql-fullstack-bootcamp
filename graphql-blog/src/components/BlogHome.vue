<template>
  <div class="blog-home">
    <h1>My GraphQL Blog Post Playground</h1>
    <blog-post-submit-form />
  </div>
</template>

<script>
import BlogPostSubmitForm from './BlogPostSubmitForm.vue';

export default {
  name: 'BlogHome',
  components: {
    BlogPostSubmitForm
  },
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.blog-home {
  padding: 0 25%;
}

h1 {
  text-align: center;
}
</style>
