F<template>
  <div v-if="posts.length !== 0">
    <h1>Список постов</h1>
    <post-item @remove="$emit('remove', post)" v-for="post in posts" :post="post" :key="post.id"/>
  </div>
  <div v-else>
    <h1>Список постов пуст</h1>
  </div>
</template>

<script>
import PostItem from './PostItem.vue'

export default {
  name: 'PostList',
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
h1 {
  margin: 15px 0;
}
</style>
