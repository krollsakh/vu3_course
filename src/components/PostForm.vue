<template>
  <form @submit.prevent>
    <my-input class="input" type="text" placeholder="Тема" v-model="post.title"/>
    <my-input class="input" type="text" placeholder="Описание" v-model="post.body"/>
    <my-button @click="createPost" style="align-self: flex-end; margin-top: 10px">
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

.input {
  width: 100%;
  margin-top: 10px;
  padding: 10px;
  border: 1px solid #0279F0FF;
}

</style>
