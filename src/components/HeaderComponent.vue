<template>
  <header >
      <nav class="navbar navbar-expand-lg container">
          <div class="container-fluid">
              <router-link to="/" class="navbar-brand" id="logo">
                  <i class="fa-solid fa-store"></i>MyBoolpress
              </router-link>

              <button class="navbar-toggler bg-white text-secondary" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
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
                // nome presente nel name del router
                routeName: 'home'
              },
              {
                label: 'Posts',
                routeName: 'posts'
              },
              {
                label: 'About',
                routeName: 'about-us'
              },
              {
                label: 'Contact',
                routeName: 'contact'
              },
          ],
          show: false
      }
  }
}
</script>

<style lang="scss" scoped>
.nav-link.router-link-active {
  color: #3e6ef1;
}
header {
  background-color: rgb(61, 61, 61, 0.8);
  height: 100px;
  font-size: 20px;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 999;
  display: flex;
  nav {
  #logo{
      color: white !important; 
      font-size: 25px;
      font-weight: bold;
    }
  a {
    color: white;
    &:not(#logo):hover { 
      color:  #2455db !important;
    }
  }
}

}


</style>
                                                                                                         