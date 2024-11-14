<template>
  <nav class="navbar">
    <div class="container">
      <router-link to="/">
        <a class="navbar-brand" href="#">
          <img
            src="../assets/harry-potter-svgrepo-com.png"
            alt="Bootstrap"
          />
        </a>
      </router-link>

      <li class="nav-item">
        <router-link to="/about"
          ><a class="nav-link active" aria-current="page">About</a></router-link
        >
      </li>
    </div>
  </nav>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>

<style scoped>
a {
  text-decoration: none;
  color: rgb(255, 255, 255);
}

a img {
  height: 2rem;
}

img {
  width: 3rem;
}

nav {
  background-color: #101010;
}

a:hover{
  color: rgba(255, 255, 255, 0.575);
}
</style>