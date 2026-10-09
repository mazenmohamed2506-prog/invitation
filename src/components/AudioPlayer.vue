<template>
  <button
    class="audio-fab"
    :class="{ 'is-playing': isPlaying }"
    @click="toggleAudio"
    aria-label="Toggle background music"
  >
    <svg
      class="audio-fab__icon"
      :class="{ 'audio-fab__icon--spinning': isPlaying }"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="1.5"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <template v-if="isPlaying">
        <circle cx="12" cy="12" r="10" />
        <circle cx="12" cy="12" r="3" />
        <line x1="12" y1="2" x2="12" y2="5" />
        <line x1="12" y1="19" x2="12" y2="22" />
        <line x1="2" y1="12" x2="5" y2="12" />
        <line x1="19" y1="12" x2="22" y2="12" />
      </template>
      <template v-else>
        <path d="M9 18V5l12-2v13" />
        <circle cx="6" cy="18" r="3" />
        <circle cx="18" cy="16" r="3" />
      </template>
    </svg>
  </button>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

let audio = null
const isPlaying = ref(false)

function handleVisibilityChange() {
  if (!audio) return
  if (document.hidden) {
    // User left the tab / minimized — pause the music
    audio.pause()
  } else {
    // User came back — resume if it was playing
    if (isPlaying.value) {
      audio.play().catch(() => {})
    }
  }
}

onMounted(() => {
  audio = new Audio('/music/audiomass-output.mp3')
  audio.loop = true
  audio.preload = 'auto'
  
  // Attempt to play automatically since the user just clicked "Open" on the envelope
  audio.play().then(() => {
    isPlaying.value = true
  }).catch((e) => {
    // Autoplay was blocked (e.g., strict browser policies)
    console.warn("Autoplay blocked:", e)
  })

  // Listen for tab visibility changes
  document.addEventListener('visibilitychange', handleVisibilityChange)
})

onBeforeUnmount(() => {
  // Stop and clean up audio when component is destroyed
  if (audio) {
    audio.pause()
    audio.src = ''
    audio = null
  }
  document.removeEventListener('visibilitychange', handleVisibilityChange)
})

function toggleAudio() {
  if (!audio) return

  if (isPlaying.value) {
    audio.pause()
  } else {
    audio.play().catch(() => {
      // Autoplay blocked — user must interact first
    })
  }
  isPlaying.value = !isPlaying.value
}
</script>

<style scoped>
.audio-fab {
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  z-index: 1000;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  border: 1.5px solid var(--color-gold);
  background: var(--color-navy);
  color: var(--color-ivory);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 20px rgba(74, 20, 26, 0.4);
}

.audio-fab:hover {
  background: var(--color-navy-dark);
  transform: scale(1.1);
}

.audio-fab.is-playing {
  border-color: var(--color-gold-light);
  box-shadow: 0 4px 20px rgba(196, 164, 155, 0.4);
}

.audio-fab__icon {
  width: 22px;
  height: 22px;
  transition: transform 0.3s ease;
}

.audio-fab__icon--spinning {
  animation: spinSlow 3s linear infinite;
}
</style>
