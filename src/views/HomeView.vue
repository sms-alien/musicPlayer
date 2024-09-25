<template>

  <template v-for="item in songList" :key="item.id">
    <div class="songs">
      <div class="albumPic">
        <img :src="item.image[2].url" alt="song-cover">
      </div>

      <div class="details">
        <h3>{{ item.name }} </h3>
        <p>{{ item.artists.all[0].name }}</p>
      </div>

      <div class="actions">
        <Icon @click="(isPlaying && source.current  == item.id) ? pauseSong() : setPlay(item)" :icon="(isPlaying && source.current  == item.id) ? 'mdi:pause' : 'mdi:play-outline'" />
      </div>

    </div>
  </template>

</template>

<script setup>
import { Icon } from '@iconify/vue';
import { onMounted, reactive, ref } from 'vue';

let audio = null
const isPlaying = ref(false)
const source = reactive({
  audio: null,
  current: null
})

const songList = ref([])

onMounted(() => {
  fetchsong()
})

const fetchsong = async() => {
  try {
    const res = await fetch('https://jio-api-ten.vercel.app/api/songs/yDeAS8Eh/suggestions', { method: 'GET' })
    const data = await res.json();

    songList.value = data.data;

  } catch (error) {
    console.log(error);
  }
}

function setPlay(params) {

  if (source.audio) {
    source.audio.pause()
    source.audio.currentTime = 0
  }

  source.current = params.id
  source.audio = new Audio(params.downloadUrl[2].url);
  source.audio.play();
  isPlaying.value = true

}

function pauseSong() {
  source.audio.pause()
  isPlaying.value = false
}

</script>

<style scoped>
.songs {
  width: 75%;
  background-color: rgb(6, 194, 106);
  margin: 4px auto;
  border-radius: 12px;
  display: flex;
  position: relative;
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

img {
  object-fit: cover;
  height: 100%;
  width: 100%;
  border-radius: 12px 0 0 12px;
}

.details {
  margin: 1.5em;
}

.actions {
  right: 2em;
  position: absolute;
  font-size: 2rem;
  display: flex;
  margin: 2.5% auto;
}
</style>
