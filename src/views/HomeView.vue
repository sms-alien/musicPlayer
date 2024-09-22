<template>
  <div class="songs">
    <div class="albumPic">Album Pic</div>
    <div class="details">
      <h3>Title</h3>
      <p>author</p>
    </div>
  </div>
</template>

<script setup>
import { walkIdentifiers } from "vue/compiler-sfc";

async function song() {
  let res = await fetch('https://saavn.dev/modules?language=english',{method:'GET'})
  let data =await res.json();
  console.log(data); 
}

song()
</script>

<style scoped>
.songs {
  min-width: 90%;
  background-color: rgb(6, 194, 106);
  margin: 4px auto;
  border-radius: 12px;
  display: flex;
}

.albumPic {
  height: 100px;
  width: 100px;
  background-color: rgb(207, 199, 189);
  border-radius: 12px;
  justify-content: center;
  align-items: center;
  display: flex;
}
.details{
  margin: 1.5em;
}
</style>
