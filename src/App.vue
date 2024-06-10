<template>
  <div class="bg-light">
      <HeaderComponent></HeaderComponent>
    <main class="container">
      <!-- <ul>
        <li v-for="(item, index) in menuItems" :key="index">
          <router-link :to="{ name: item.routeName }" class="nav-link">
            {{ item.label }}
          </router-link>
        </li>
      </ul> -->
      <!-- dove viene caricato il contenuto delle rotte -->
      <router-view></router-view>
    </main>
  </div>
</template>

<script>
  import HeaderComponent from './components/HeaderComponent.vue'
  export default {
    components: {
      HeaderComponent
    },
    name: "App",
    data() {
      return {
        // menuItems: [
        //   {
        //     label: "home",
        //     routeName: "AppHome",
        //   },
        //   {
        //     label: "posts",
        //     routeName: "PostList",
        //   },
        // ],
      };
    },
  }
</script>

<style lang="scss" scoped>

</style>