<template>
    <div>
      <h1 class="text-center">Post</h1>
      <div class="container">
        <div class="row">
          <div class="col-md-3 mb-4" v-for="post in posts" :key="post.id">
            <div class="card h-100">
              <img :src="store.imgBasePath + post.image" class="card-img-top" :alt="post.title">
              <div class="card-body">
                <h5 class="card-title">{{ post.title }}</h5>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { store } from '../store';
  import axios from 'axios';
  export default {
    name: 'PostList',
    data() {
      return {
        store,
        posts: [],
  
      }
    },
    methods: {
      getAllPosts() {
        axios.get(this.store.apiBaseUrl + '/posts').then((res) => {
          console.log(res.data);
          this.posts = res.data.results;
          //se paginazione
          //this.posts = res.data.results.data;
          //this.currentPage = res.data.results.current_page;
        });
      },
    },
    mounted() {
      this.getAllPosts();
    }
  }
  </script>
  
  <style lang="scss" scoped></style>