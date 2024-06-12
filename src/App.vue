<template>

  <HeaderComponent />
  <main class="container my-4">
    <router-view></router-view>
  </main>

  <ul class="circles">
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
  
</template>



<script>
import HeaderComponent from './components/HeaderComponent.vue'
import { store } from './store.js'
import axios from 'axios';
export default {
  name: 'App',
  components: {
    HeaderComponent
  },
  data() {
    return {
      store
    }
  },
  methods: {
    getCategories() {
      axios.get(this.store.apiBaseUrl + '/categories').then((res) => {
        console.log(res.data);
        this.store.categories = res.data.results;
      });
    }
  },
  mounted() {
    this.getCategories();
  },
}
</script>

<style lang="scss" scoped></style>