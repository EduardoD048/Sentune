<script setup>
import { ref } from "vue";
import Navbar from "./components/Navbar.vue";
import Player from "./components/player.vue";
import Playlist from "./components/Playlist.vue";

// Playlist compartilhada entre os componentes
const allMusics = ref([
  {
    id: 1,
    name: "Sample Audio Track",
    artist: "Demo Artist",
    duration: "0:30",
    src: "https://www.soundjay.com/misc/sounds/bell-ringing-05.wav",
    cover: "https://via.placeholder.com/300x300/1db954/ffffff?text=Music+1",
  },
  {
    id: 2,
    name: "Test Song",
    artist: "Test Artist",
    duration: "1:00",
    src: "https://file-examples.com/storage/fe86a9b4d9320d51ab21ebb/2017/11/file_example_MP3_700KB.mp3",
    cover: "https://via.placeholder.com/300x300/8b5cf6/ffffff?text=Music+2",
  },
  {
    id: 3,
    name: "Demo Track",
    artist: "Sample Artist",
    duration: "0:45",
    src: "https://www.soundjay.com/misc/sounds/beep-07a.wav",
    cover: "https://via.placeholder.com/300x300/0ea5e9/ffffff?text=Music+3",
  },
  {
    id: 4,
    name: "Audio Sample",
    artist: "Demo Band",
    duration: "1:30",
    src: "https://file-examples.com/storage/fe86a9b4d9320d51ab21ebb/2017/11/file_example_MP3_1MG.mp3",
    cover: "https://via.placeholder.com/300x300/f59e0b/ffffff?text=Music+4",
  },
  {
    id: 5,
    name: "Sound Test",
    artist: "Audio Artist",
    duration: "0:20",
    src: "https://www.soundjay.com/misc/sounds/beep-10.wav",
    cover: "https://via.placeholder.com/300x300/ef4444/ffffff?text=Music+5",
  },
]);
</script>

<template>
  <Navbar />
  <Playlist :playlist="allMusics" />
  <Player :playlist="allMusics" />
</template>
