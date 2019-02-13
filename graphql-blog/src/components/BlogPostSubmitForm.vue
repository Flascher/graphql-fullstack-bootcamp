<template>
  <form class="blog-post-submit-form">
    <input
      type="text"
      class="blog-post-title-input"
      placeholder="Post Title..."
      v-model="postTitle"
    />
    <select class="blog-post-author-select" v-model="selectedUserId">
      <option
        v-for="author in authorNames"
        :key="author.id"
        :label="`${author.firstName} ${author.lastName}`"
        :value="author.id"
      ></option>
    </select>
    <textarea
      class="blog-post-content-input"
      placeholder="Post Content..."
      v-model="postContent"
    ></textarea>
    <button class="blog-post-submit-button" @click.prevent="submitForm">
      Submit Post
    </button>
  </form>
</template>

<script>
import UserFirstAndLast from '../graphql/queries/UserFirstAndLast.gql';
import AllPosts from '../graphql/queries/AllPosts.gql';
import AddPost from '../graphql/mutations/AddPost.gql';

export default {
  name: 'BlogPostSubmitForm',
  apollo: {
    authorNames: UserFirstAndLast
  },
  data() {
    return {
      postTitle: '',
      postContent: '',
      selectedUserId: ''
    };
  },
  methods: {
    submitForm() {
      const subject = this.postTitle;
      const content = this.postContent;

      // reset form on submit
      this.postTitle = '';
      this.postContent = '';

      this.$apollo
        .mutate({
          // Query
          mutation: AddPost,
          // Parameters
          variables: {
            subject,
            content,
            userId: this.selectedUserId
          },
          // Update the cache with the result
          // The query will be updated with the optimistic response
          // and then with the real result of the mutation
          update: (store, { data: { addedPost } }) => {
            // Read the data from our cache for this query.
            const data = store.readQuery({ query: AllPosts });
            // Add our tag from the mutation to the end
            data.posts.push(addedPost);
            // Write our data back to the cache.
            store.writeQuery({ query: AllPosts, data });
          }
          // Optimistic UI
          // Will be treated as a 'fake' result as soon as the request is made
          // so that the UI can react quickly and the user be happy
          // optimisticResponse: {
          //   __typename: 'Mutation',
          //   addPost: {
          //     __typename: 'Post',
          //     id: -1,
          //     label: subject
          //   }
          // }
        })
        .then(data => {
          // Result
          console.log(data);
          debugger;
        })
        .catch(error => {
          // Error
          console.error(error);
          debugger;
        });
    }
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
  margin-bottom: 15px;
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

.blog-post-submit-button {
  grid-row: 10;
  grid-column: 8 / 10;
}
</style>
