<template>
 <header>
  <nav class="navbar navbar-expand-lg container">
    <div class="container-fluid ">
      <a class="navbar-brand"  id="logo" href="\">Boolfolio</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          <li class="nav-item">
            <!-- <a class="nav-link"  aria-current="page" href="\">Home</a> -->
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <!-- <a class="nav-link" href="/posts">Posts</a> -->
            <router-link class="nav-link" to="/posts">Posts</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
 </header>
</template>

<script>
  export default {
    name: "HeaderComponent",
  }
</script>

<style lang="scss" scoped>
.nav-link.router-link-active {
  color: rgb(229, 252, 21);
}
header {
  background-color: rgb(61, 61, 61);
  nav {
  #logo:hover {
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