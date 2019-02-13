<template>
  <form class="blog-post-submit-form">
    <input type="text" class="blog-post-title-input" placeholder="Post Title...">
    <select class="blog-post-author-select">
      <option
        v-for="author in authorNames"
        :key="author.id"
        :label="`${author.firstName} ${author.lastName}`"
        :value="author.id"
      ></option>
    </select>
    <textarea class="blog-post-content-input" placeholder="Post Content..."></textarea>
  </form>
</template>

<script>
import UserFirstAndLastQuery from '../graphql/queries/UserFirstAndLast.gql';

export default {
  name: 'BlogPostSubmitForm',
  apollo: {
    authorNames: UserFirstAndLastQuery
  }
};
</script>

<style lang="scss" scoped>
.blog-post-submit-form {
  display: grid;
  grid-template-columns: 25px;
  grid-template-rows: 25px;
  row-gap: 15px;
  column-gap: 15px;
  height: 150px;
}

.blog-post-title-input {
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row: 1;
}

.blog-post-author-select {
  grid-column-start: 4;
  grid-column-end: 10;
  grid-row: 1;
}

.blog-post-content-input {
  grid-row: 2 / 10;
  grid-column: 1 / 10;
  font: inherit;
}
</style>
