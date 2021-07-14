<template>
  <form @submit.prevent>
    <my-input  type="text" placeholder="Тема" v-model="post.title"/>
    <my-input  type="text" placeholder="Описание" v-model="post.body"/>
    <my-button @click="createPost" style="align-self: flex-end">
      Добавить пост
    </my-button>
  </form>
</template>

<script>
export default {
  name: 'PostForm',
  data () {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost () {
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>
