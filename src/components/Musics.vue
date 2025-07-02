<template>
  <div class="music-container">
    <div class="music-item" v-for="music in musics" :key="music.id">
      <div class="music-info">
        <span class="song-name">{{ music.name }}</span>
        <span class="artist-name">{{ music.artist }}</span>
      </div>
      <span class="duration">{{ music.duration }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Music",
  props: {
    musics: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.music-container {
  width: 100%;
  max-height: 400px;
  overflow-y: auto;
  padding: 10px;
}

.music-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.music-item:hover {
  background-color: #f5f5f5;
}

.music-info {
  display: flex;
  flex-direction: column;
}

.song-name {
  font-weight: 500;
  color: #b3b3b3;
  margin-bottom: 4px;
}

.artist-name {
  font-size: 14px;
  color: #b3b3b3;;
}

.duration {
  font-size: 14px;
  color: #b3b3b3;
}
</style>
