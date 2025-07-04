<template>
  <div class="player-container">
    <!-- Informações da música atual -->
    <div class="music-info">
      <img :src="currentMusic.cover" alt="Capa" class="music-cover" />
      <div class="music-details">
        <span class="song-name">{{ currentMusic.name }}</span>
        <span class="artist-name">{{ currentMusic.artist }}</span>
      </div>
    </div>

    <!-- Controles centrais -->
    <div class="player-controls">
      <!-- Botões de controle -->
      <div class="control-buttons">
        <button @click="previousTrack" class="control-btn">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
            <path
              d="M3.3 1a.7.7 0 0 1 .7.7v5.15l9.95-5.744a.7.7 0 0 1 1.05.606v12.588a.7.7 0 0 1-1.05.606L4 8.149V13.3a.7.7 0 0 1-1.4 0V1.7a.7.7 0 0 1 .7-.7z"
            />
          </svg>
        </button>

        <button @click="togglePlay" class="control-btn play-btn">
          <svg
            v-if="!isPlaying"
            width="16"
            height="16"
            viewBox="0 0 16 16"
            fill="currentColor"
          >
            <path
              d="m11.596 8.697-6.363 3.692c-.54.313-1.233-.066-1.233-.697V4.308c0-.63.692-1.01 1.233-.696l6.363 3.692a.802.802 0 0 1 0 1.393z"
            />
          </svg>
          <svg
            v-else
            width="16"
            height="16"
            viewBox="0 0 16 16"
            fill="currentColor"
          >
            <path
              d="M5.5 3.5A1.5 1.5 0 0 1 7 2h2a1.5 1.5 0 0 1 1.5 1.5v9A1.5 1.5 0 0 1 9 14H7a1.5 1.5 0 0 1-1.5-1.5v-9z"
            />
          </svg>
        </button>

        <button @click="nextTrack" class="control-btn">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
            <path
              d="M12.7 1a.7.7 0 0 0-.7.7v5.15L2.05 1.107A.7.7 0 0 0 1 1.712v12.588a.7.7 0 0 0 1.05.606L12 8.149V13.3a.7.7 0 0 0 1.4 0V1.7a.7.7 0 0 0-.7-.7z"
            />
          </svg>
        </button>
      </div>

      <!-- Barra de progresso -->
      <div class="progress-container">
        <span class="time-display">{{ formatTime(currentTime) }}</span>
        <div class="progress-bar" @click="seekTo">
          <div class="progress-track">
            <div
              class="progress-fill"
              :style="{ width: progressPercentage + '%' }"
            ></div>
            <div
              class="progress-handle"
              :style="{ left: progressPercentage + '%' }"
            ></div>
          </div>
        </div>
        <span class="time-display">{{ formatTime(duration) }}</span>
      </div>
    </div>

    <!-- Controle de volume -->
    <div class="volume-control">
      <button @click="toggleMute" class="volume-btn">
        <svg
          v-if="volume > 0.5"
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="currentColor"
        >
          <path
            d="M11.536 14.01A8.473 8.473 0 0 0 14.026 8a8.473 8.473 0 0 0-2.49-6.01l-.708.707A7.476 7.476 0 0 1 13.025 8c0 2.071-.84 3.946-2.197 5.303l.708.707z"
          />
          <path
            d="M10.121 12.596A6.48 6.48 0 0 0 12.025 8a6.48 6.48 0 0 0-1.904-4.596l-.707.707A5.483 5.483 0 0 1 11.025 8a5.483 5.483 0 0 1-1.61 3.89l.706.706z"
          />
          <path
            d="M8.707 11.182A4.486 4.486 0 0 0 10.025 8a4.486 4.486 0 0 0-1.318-3.182L8 5.525A3.489 3.489 0 0 1 9.025 8 3.49 3.49 0 0 1 8 10.475l.707.707zM6.717 3.55A.5.5 0 0 1 7 4v8a.5.5 0 0 1-.812.39L3.825 10.5H1.5A.5.5 0 0 1 1 10V6a.5.5 0 0 1 .5-.5h2.325l2.363-1.89a.5.5 0 0 1 .529-.06z"
          />
        </svg>
        <svg
          v-else-if="volume > 0"
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="currentColor"
        >
          <path
            d="M9 4a.5.5 0 0 0-.812-.39L5.825 5.5H3.5A.5.5 0 0 0 3 6v4a.5.5 0 0 0 .5.5h2.325l2.363 1.89A.5.5 0 0 0 9 12V4z"
          />
          <path
            d="m9.975 8.5a3.5 3.5 0 0 0-1.146-2.626l-.708.708a2.5 2.5 0 0 1 0 3.836l.708.708A3.5 3.5 0 0 0 9.975 8.5z"
          />
        </svg>
        <svg
          v-else
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="currentColor"
        >
          <path
            d="M6.717 3.55A.5.5 0 0 1 7 4v8a.5.5 0 0 1-.812.39L3.825 10.5H1.5A.5.5 0 0 1 1 10V6a.5.5 0 0 1 .5-.5h2.325l2.363-1.89a.5.5 0 0 1 .529-.06zm7.137.427A.5.5 0 0 1 14 4.5v7a.5.5 0 0 1-.854.354l-1.853-1.853a.5.5 0 0 1 0-.708l1.853-1.853a.5.5 0 0 1 .708 0z"
          />
        </svg>
      </button>

      <div class="volume-slider">
        <input
          type="range"
          min="0"
          max="1"
          step="0.01"
          v-model="volume"
          @input="updateVolume"
          class="volume-input"
        />
      </div>
    </div>

    <!-- Elemento audio (oculto) -->
    <audio
      ref="audioPlayer"
      @timeupdate="updateTime"
      @loadedmetadata="updateDuration"
      @ended="nextTrack"
    ></audio>
  </div>
</template>

<script>
export default {
  name: "Player",
  props: {
    playlist: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      currentTrackIndex: 0,
      isPlaying: false,
      currentTime: 0,
      duration: 0,
      volume: 0.7,
      previousVolume: 0.7,
    };
  },
  computed: {
    currentMusic() {
      return (
        this.playlist[this.currentTrackIndex] || {
          name: "Nenhuma música",
          artist: "Selecione uma música",
          cover: "https://via.placeholder.com/60x60/333/fff?text=♪",
        }
      );
    },
    progressPercentage() {
      if (this.duration === 0) return 0;
      return (this.currentTime / this.duration) * 100;
    },
  },
  watch: {
    currentTrackIndex() {
      this.loadCurrentTrack();
    },
    playlist() {
      if (this.playlist.length > 0) {
        this.loadCurrentTrack();
      }
    },
  },
  mounted() {
    if (this.playlist.length > 0) {
      this.loadCurrentTrack();
    }
  },
  methods: {
    loadCurrentTrack() {
      if (this.currentMusic.src) {
        this.$refs.audioPlayer.src = this.currentMusic.src;
        this.$refs.audioPlayer.volume = this.volume;
      }
    },
    togglePlay() {
      if (this.isPlaying) {
        this.$refs.audioPlayer.pause();
      } else {
        this.$refs.audioPlayer.play();
      }
      this.isPlaying = !this.isPlaying;
    },
    previousTrack() {
      if (this.currentTrackIndex > 0) {
        this.currentTrackIndex--;
      } else {
        this.currentTrackIndex = this.playlist.length - 1;
      }
      this.isPlaying = false;
    },
    nextTrack() {
      if (this.currentTrackIndex < this.playlist.length - 1) {
        this.currentTrackIndex++;
      } else {
        this.currentTrackIndex = 0;
      }
      this.isPlaying = false;
    },
    seekTo(event) {
      const progressBar = event.currentTarget;
      const clickX = event.offsetX;
      const width = progressBar.offsetWidth;
      const newTime = (clickX / width) * this.duration;
      this.$refs.audioPlayer.currentTime = newTime;
    },
    updateTime() {
      this.currentTime = this.$refs.audioPlayer.currentTime;
    },
    updateDuration() {
      this.duration = this.$refs.audioPlayer.duration;
    },
    updateVolume() {
      this.$refs.audioPlayer.volume = this.volume;
    },
    toggleMute() {
      if (this.volume > 0) {
        this.previousVolume = this.volume;
        this.volume = 0;
      } else {
        this.volume = this.previousVolume;
      }
      this.updateVolume();
    },
    formatTime(seconds) {
      if (isNaN(seconds)) return "0:00";
      const mins = Math.floor(seconds / 60);
      const secs = Math.floor(seconds % 60);
      return `${mins}:${secs.toString().padStart(2, "0")}`;
    },
  },
};
</script>

<style scoped>
.player-container {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 90px;
  background-color: #181818;
  border-top: 1px solid #282828;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 16px;
  z-index: 1000;
}

/* Informações da música */
.music-info {
  display: flex;
  align-items: center;
  min-width: 180px;
  width: 30%;
}

.music-cover {
  width: 56px;
  height: 56px;
  border-radius: 4px;
  margin-right: 14px;
}

.music-details {
  display: flex;
  flex-direction: column;
  min-width: 0;
}

.song-name {
  color: #ffffff;
  font-size: 14px;
  font-weight: 400;
  margin-bottom: 4px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.artist-name {
  color: #b3b3b3;
  font-size: 11px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Controles centrais */
.player-controls {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
  max-width: 722px;
}

.control-buttons {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 8px;
}

.control-btn {
  background: none;
  border: none;
  color: #b3b3b3;
  cursor: pointer;
  padding: 8px;
  border-radius: 50%;
  transition: color 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.control-btn:hover {
  color: #ffffff;
}

.play-btn {
  background-color: #ffffff;
  color: #000000;
  width: 32px;
  height: 32px;
  padding: 0;
}

.play-btn:hover {
  background-color: #ffffff;
  transform: scale(1.06);
}

/* Barra de progresso */
.progress-container {
  display: flex;
  align-items: center;
  width: 100%;
  gap: 12px;
}

.time-display {
  color: #b3b3b3;
  font-size: 11px;
  min-width: 40px;
  text-align: center;
}

.progress-bar {
  flex: 1;
  cursor: pointer;
  padding: 4px 0;
}

.progress-track {
  position: relative;
  height: 4px;
  background-color: #5e5e5e;
  border-radius: 2px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background-color: #1db954;
  border-radius: 2px;
  transition: width 0.1s linear;
}

.progress-handle {
  position: absolute;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 12px;
  height: 12px;
  background-color: #ffffff;
  border-radius: 50%;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.progress-bar:hover .progress-handle {
  opacity: 1;
}

.progress-bar:hover .progress-track {
  background-color: #727272;
}

/* Controle de volume */
.volume-control {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  min-width: 180px;
  width: 30%;
  gap: 8px;
}

.volume-btn {
  background: none;
  border: none;
  color: #b3b3b3;
  cursor: pointer;
  padding: 8px;
  border-radius: 4px;
  transition: color 0.2s ease;
}

.volume-btn:hover {
  color: #ffffff;
}

.volume-slider {
  width: 93px;
}

.volume-input {
  width: 100%;
  height: 4px;
  background: #5e5e5e;
  border-radius: 2px;
  outline: none;
  cursor: pointer;
  appearance: none;
  -webkit-appearance: none;
}

.volume-input::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 12px;
  height: 12px;
  background: #ffffff;
  border-radius: 50%;
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.volume-slider:hover .volume-input::-webkit-slider-thumb {
  opacity: 1;
}

.volume-input::-moz-range-thumb {
  width: 12px;
  height: 12px;
  background: #ffffff;
  border-radius: 50%;
  cursor: pointer;
  border: none;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.volume-slider:hover .volume-input::-moz-range-thumb {
  opacity: 1;
}

/* Responsividade */
@media (max-width: 768px) {
  .player-container {
    padding: 0 8px;
  }

  .music-info,
  .volume-control {
    min-width: 120px;
    width: 25%;
  }

  .volume-slider {
    width: 60px;
  }
}
</style>
