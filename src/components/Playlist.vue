<template>
  <div class="playlist">
    <h1>Playlist</h1>
    <div class="last-listen-sidebar"><button>ultima escutada</button></div>
    <div class="recommended"><button>recomendada</button></div>

    <!-- Componente filho recebendo músicas via prop -->
    <Musics :musics="playlistMusics" />
  </div>
</template>

<script>
import Musics from "./Musics.vue";

export default {
  name: "Playlist",
  components: {
    Musics,
  },
  data() {
    return {
      playlistMusics: [
        { id: 1, name: "Bohemian Rhapsody", artist: "Queen", duration: "5:55" },
        { id: 2, name: "Hotel California", artist: "Eagles", duration: "6:30" },
        { id: 3, name: "Imagine", artist: "John Lennon", duration: "3:07" },
        { id: 4, name: "Stairway to Heaven",artist: "Led Zeppelin", duration: "8:02",},
        { id: 5,name: "Sweet Child O Mine",artist: "Guns N Roses", duration: "5:03",},
      ],
    };
  },
};
</script>

<style scoped>
.playlist {
  display: flex;
  width: 20%;
  height: 100vh;
  background-color: rgb(69, 101, 243);
  flex-direction: column;
}

.playlist h1 {
  color: #b3b3b3;
  font-size: 28px;
  margin-bottom: 26px;
  margin-left: 20px;
  margin-top: 26px;
}

.playlist button {
  background-color: #121212;
  color: #b3b3b3;
  border: none;
  padding: 16px;
  border-radius: 500px;
  cursor: pointer;
  margin: 10px;
}

.playlist button:hover {
  background-color: #5de7ff;
}
</style>
