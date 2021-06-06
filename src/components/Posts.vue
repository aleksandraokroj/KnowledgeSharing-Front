<template>
  <div>
    <div v-bind:key="post.id" v-for="post in posts">
      <PostItem v-bind:id="post.id" v-bind:title="post.title"
       v-bind:post="post" v-on:del-post="$emit('del-post', post.id)"
       v-bind:posts="posts"/>
    </div>
  </div>
</template>

<script>
import PostItem from './PostItem.vue';
export default {
  name: "Posts",
  components: {
    PostItem
  },
  props: ["posts"]
}
</script>

<style scoped>
</style>