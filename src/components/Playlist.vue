<template>
  <div class="playlist">
    <h1>Playlist</h1>
    <div class="last-listen-sidebar"><button>ultima escutada</button></div>
    <div class="recommended"><button>recomendada</button></div>

    <!-- Componente filho recebendo músicas via prop -->
    <Musics :musics="playlist" />
  </div>
</template>

<script>
import Musics from "./Musics.vue";

export default {
  name: "Playlist",
  components: {
    Musics,
  },
  props: {
    playlist: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.playlist {
  display: flex;
  width: 20%;
  height: 100vh;
  background-color: rgb(251, 255, 252);
  flex-direction: column;
  background-color: #151a57;
}

.playlist h1 {
  color: #b3b3b3;
  font-size: 28px;
  margin-bottom: 26px;
  margin-left: 20px;
  margin-top: 26px;
}

.playlist button {
  color: #b3b3b3;
  border: none;
  padding: 16px;
  border-radius: 500px;
  cursor: pointer;
  margin: 10px;
  background: transparent;
}
</style>
