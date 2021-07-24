F
<template>
  <div v-if="posts.length !== 0">
    <h1>Список постов</h1>
    <transition-group name="post-list">
      <post-item @remove="$emit('remove', post)" v-for="post in posts" :post="post" :key="post.id"/>
    </transition-group>
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

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}

.post-list-enter-active,
.post-list-leave-active {
  transition: all .5s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.post-list-move {
  transition: transform 0.5s ease;
}
</style>
