<template>
  <nav>
    <h1>Music Player</h1>
    <span>
    <RouterLink to="/">Home</RouterLink>
  </span>
  </nav>
  <RouterView />
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HomeViewVue from './views/HomeView.vue'
</script>

<style>
nav{
  background-color: rgb(93, 245, 194);
  display: flex;
  text-shadow: 2px 2px black;
  height: 5rem;
  align-items: center;
  margin-bottom: 2em;
}
body{
  background-color: rgb(119, 219, 186);
  color: snow;
  
}
span{
  right: 2em;
  position: absolute;
  text-shadow: none;
  font-size: 1.5em;
}
nav>h1{
  left: 3em;
  position: relative;
}
</style>
