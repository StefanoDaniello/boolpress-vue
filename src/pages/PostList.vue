<template>
  <div class="d-flex justify-content-between align-items-center">
      <h1>All Posts</h1>
      <select name="categories" id="categories" class="form-select w-25">
          <option value="">Tutte le categorie</option>
          <option value="category.id" v-for="category in store.categories" :key="category.id">{{ category.name }}
          </option>
      </select>
  </div>

  <div class="row">
      <div class="col-12 col-lg-6" v-for="post in posts" :key="post.id">
        <CardComponent :item="post" />
       </div>    
    </div>

    <nav aria-label="..." class="d-flex justify-content-center mt-1">
        <ul class="pagination">
            <li class="page-item ">
                <a class="page-link" :class="{'disabled' : currentPage <= 1}" href="#" 
                @click.prevent="setParams(currentPage-1)">Previous</a>
            </li>
            <li class="page-item" v-for="page in totalPage" :key="page">
                <a class="page-link" :class="{ 'active': currentPage == page }" href="#"
                    @click.prevent="setParams(page)">{{ page }}</a>
            </li>
            <li class="page-item">
                <a class="page-link" :class="{'disabled' : currentPage >= totalPage}" href="#"
                    @click.prevent="setParams(currentPage+1)">Next</a>
            </li>
        </ul>
    </nav>
</template>

<script>
import { store } from '../store';
import axios from 'axios';
import CardComponent from '../components/CardComponent.vue';

export default {
  name: 'PostList',
  components: {
      CardComponent
  },
  data() {
    return {
      store,
      posts: [],
      currentPage: 0,
      totalPage: 0,
      params:null,
    }
  },
  methods: {
    setParams(numpage) {
        this.current_page = numpage;
        this.params={
            page: this.current_page
        }
        this.getAllPosts();
    },
    getAllPosts() {
        // if(this.currentPage){
        //     this.params = {
        //     page: this.currentPage
        //     }
        // }
        axios.get(this.store.apiBaseUrl + '/posts',{params: this.params}).then((res) => {
        console.log(res.data);
        //this.posts = res.data.results;
        //con la paginazione
        this.posts = res.data.results.data;
        this.currentPage = res.data.results.current_page;
        this.totalPage = res.data.results.last_page;
        this.params=null;
    });
    },
    // nextPage() {
    //     this.currentPage+=1;
    //     this.getAllPosts();
    // },
    // previewPage() {
    //     this.currentPage-=1;
    //     this.getAllPosts();
    // },
    // changePage(page) {
    //     this.currentPage = page;
    //     this.getAllPosts();
    // } 
  },
  mounted() {
    this.getAllPosts();
  },

}

</script>

<style lang="sass" scoped>

</style>