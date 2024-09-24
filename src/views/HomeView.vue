<template>
  <template v-for="item in songList" :key="item.id" >
    <div class="songs" @click="setPlay(item)" >
    <div class="albumPic">
      <img :src="item.image[2].url" alt="song-cover">
    </div>
    <div class="details">
      <h3>{{ item.name }} </h3>
      <p>{{item.artists.all[0].name}}</p>
    </div>
  </div>
  </template>
  
</template>

<script setup>
import { ref } from 'vue';

let audio = null
let isPlaying = false

const songList = ref([])
async function song() {
  try{
  const res = await fetch('https://jio-api-ten.vercel.app/api/songs/yDeAS8Eh/suggestions',{method:'GET'})
  const data =await res.json();

  songList.value = data.data;
  
  }catch(error){
    console.log(error);
  }
  return{
  }
}

function setPlay(params) {

  if(audio){
    audio.pause()
  }
  
  audio = new Audio(params.downloadUrl[2].url);
  audio.play();
  isPlaying = true;

  audio.onended = ()=>{ isPlaying=false}

}

song()
</script>

<style scoped>
.songs {
  width: 75%;
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

img{
  object-fit: cover;
  height: 100%;
  width: 100%;
  border-radius: 12px 0 0 12px;
}

.details{
  margin: 1.5em;
}
</style>
