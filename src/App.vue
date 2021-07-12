<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="app__btns">
      <my-button @click="showDialog">Добавить пост</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"/>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost"/>
    </my-dialog>
    <post-list v-if="!isLoadingPosts" @remove="removePost" :posts="posts"/>
    <div v-else>Идет загрузка...</div>
  </div>
</template>

<script>
import PostForm from './components/PostForm.vue'
import PostList from './components/PostList.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    PostForm,
    PostList
  },
  data () {
    return {
      posts: [],
      dialogVisible: false,
      isLoadingPosts: false,
      selectedSort: '',
      sortOptions: [
        { value: 'title', title: 'Сортировать по наименованию' },
        { value: 'body', title: 'Сортировать по содержимому' }
      ]
    }
  },
  methods: {
    createPost (newPost) {
      this.posts.push(newPost)
      this.dialogVisible = false
    },
    removePost (post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog () {
      this.dialogVisible = true
    },
    async fetchPosts () {
      try {
        this.isLoadingPosts = true
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data
      } catch (e) {
        alert('Ошибка чтения постов')
      } finally {
        this.isLoadingPosts = false
      }
    }
  },
  mounted () {
    this.fetchPosts()
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  font-size: 16px;
  font-family: sans-serif;
}

.app {
  margin: 15px;
}

h1 {
  font-size: 18px;
  margin-bottom: 15px;
}

.app__btns {
  display: flex;
  justify-content: space-between;
}

select {
  border: 1px solid #0279F0FF;
}

</style>
