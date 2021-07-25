<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <my-input v-model="searchPost" placeholder="Поиск по Теме..."/>
    <div class="app__btns">
      <my-button @click="showDialog">Добавить пост</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"/>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost"/>
    </my-dialog>
    <post-list v-if="!isLoadingPosts" @remove="removePost" :posts="searchAndSortedPost"/>
    <div v-else>Идет загрузка...</div>
    <div class="page__wrapper">
      <div
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        class="page"
        :class="{ page__active: page === pageNumber }"
        @click="onClickPage(pageNumber)"
      >
        {{ pageNumber }}
      </div>
    </div>
  </div>
</template>

<script>
import PostForm from './components/PostForm.vue'
import PostList from './components/PostList.vue'
import axios from 'axios'
import MyInput from './components/UI/MyInput'

export default {
  name: 'App',
  components: {
    MyInput,
    PostForm,
    PostList
  },
  data () {
    return {
      posts: [],
      dialogVisible: false,
      isLoadingPosts: false,
      page: 1,
      limit: 3,
      totalPages: 0,
      selectedSort: '',
      searchPost: '',
      sortOptions: [
        {
          value: 'title',
          title: 'Сортировать по наименованию'
        },
        {
          value: 'body',
          title: 'Сортировать по содержимому'
        }
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
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _limit: this.limit,
            _page: this.page
          }
        })
        this.posts = response.data
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
      } catch (e) {
        alert('Ошибка чтения постов')
      } finally {
        this.isLoadingPosts = false
      }
    },
    onClickPage (pageNumber) {
      this.page = pageNumber
    }
  },
  mounted () {
    this.fetchPosts()
  },
  computed: {
    sortedPosts () {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    searchAndSortedPost () {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchPost.toLowerCase()))
    }
  },
  watch: {
    page () {
      this.fetchPosts()
    }
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

.page__wrapper {
  display: flex;
  /*align-items: center;*/
  /*justify-content: center;*/
  margin-top: 15px;
  width: 100%;
}

.page {
  display: flex;
  border: 1px solid #0279F0FF;
  border-radius: 50%;
  width: 2em;
  height: 2em;
  margin-right: 5px;
  align-items: center;
  justify-content: center;
}

.page:hover {
  cursor: pointer;
}

.page__active {
  border: 2px solid;
  background: lightblue;
}
</style>
