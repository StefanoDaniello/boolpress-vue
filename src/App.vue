<template>
  <div>
    <h1>App</h1>
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
  export default {
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