<template>
  <header >
      <nav class="navbar navbar-expand-lg container">
          <div class="container-fluid">
              <router-link to="/" class="navbar-brand" id="logo">
                  <i class="fa-solid fa-store"></i>MyBoolpress
              </router-link>

              <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                  aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation"
                  @click="show = !show">
                  <span class="navbar-toggler-icon"></span>
              </button>
              <div class="collapse navbar-collapse" :class="{ 'show': show }" id="navbarNav">
                  <ul class="navbar-nav">
                      <li class="nav-item" v-for="(link, index) in menuItems" :key="index">
                          <!-- <a class="nav-link active" aria-current="page" href="#">Home</a> -->
                          <router-link :to="{ name: link.routeName }" class="nav-link">
                              {{ link.label }}
                          </router-link>
                      </li>

                  </ul>
                  <div class="ms-auto">
                      <a href="http://localhost:8000" class="nav-link">
                          <i class="fa-solid fa-user"></i> <span>Area Riservata</span>
                      </a>
                  </div>
              </div>
          </div>
      </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
      return {
          menuItems: [
              {
                  label: 'Home',
                  routeName: 'home'
              },
              {
                  label: 'Posts',
                  routeName: 'posts'
              },
              // {
              //   label: 'Categorie',
              //   routeName: 'categories'
              // }
          ],
          show: false
      }
  }
}
</script>

<style lang="scss" scoped>
.nav-link.router-link-active {
  color: rgb(229, 252, 21);
}
header {
  background-color: rgb(61, 61, 61);
  nav {
  #logo{
      color: white !important; 
    }
  a {
    color: white;
    &:not(#logo):hover { 
      color: rgb(174, 192, 13) !important;
    }
  }
}
}
</style>
                                                                                                         