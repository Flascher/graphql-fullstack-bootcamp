<template>
  <article class="blog-post">
    <header class="blog-post-title">
      {{ title }}
    </header>
    <section class="blog-post-content">
      {{ content }}
    </section>
    <footer class="blog-post-author">
      <div class="author-name">
        by {{ author.firstName }} {{ author.lastName }}
        <img
          class="author-avatar"
          :src="author.profile.avatarUrl"
          :alt="`${author.firstName} ${author.lastName}'s avatar`"
        />
      </div>
      <div class="footer-button-container">
        <button disabled="true">Edit</button>
        <button disabled="true">Delete</button>
      </div>
    </footer>
    <blog-post-comment v-for="comment in comments" :key="comment.id" />
  </article>
</template>

<script>
import BlogPostComment from './BlogPostComment.vue';

export default {
  name: 'BlogPost',
  components: {
    BlogPostComment
  },
  props: {
    title: String,
    content: String,
    author: Object,
    comments: Array
  }
};
</script>

<style lang="scss" scoped>
.blog-post {
  border-radius: 5px;
  border: 1px solid #2c3e50;
  padding: 15px;
  margin: 5px 0;
}

.blog-post-title {
  font-size: 1.5em;
  font-weight: bold;
  text-align: center;
  padding: 15px 0;
}

.blog-post-content {
  padding: 15px 0;
}

.blog-post-author {
  text-align: right;
}

.author-avatar {
  border-radius: 50%;
  border: 1px solid #2c3e50;
  width: 30px;
  max-width: 30px;
  height: 30px;
  max-height: 30px;
}

.footer-button-container {
  display: flex;
  justify-content: space-between;
}
</style>
