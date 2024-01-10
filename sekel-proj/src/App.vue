<template>
  <div id="app">
    <BlogPosts msg="SEKEL TECH - Coding Challenge"/>
  </div>
</template>

<script>
import BlogPosts from './components/BlogPosts.vue'

export default {
  name: 'App',
  components: {
    BlogPosts
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
