<template>
  <div id="app">
    <BlogHome />
  </div>
</template>

<script>
import BlogHome from './components/BlogHome';

export default {
  name: 'app',
  components: {
    BlogHome
  }
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
