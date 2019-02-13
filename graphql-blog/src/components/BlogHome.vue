<template>
  <div class="blog-home">
    <h1>My GraphQL Blog Post Playground</h1>
    <blog-post-submit-form />
    <blog-post
      v-for="post in posts"
      :key="post.id"
      :title="post.subject"
      :content="post.content"
      :author="post.user"
      :comments="post.comments"
    />
  </div>
</template>

<script>
import AllPosts from '../graphql/queries/AllPosts.gql';

import BlogPostSubmitForm from './BlogPostSubmitForm.vue';
import BlogPost from './BlogPost.vue';

export default {
  name: 'BlogHome',
  components: {
    BlogPostSubmitForm,
    BlogPost
  },
  apollo: {
    posts: AllPosts
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
