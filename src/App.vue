<template>
  <div class="app">
    <!-- Preloader -->
    <Preloader v-if="showPreloader" @loaded="onPreloaderDone" />

    <!-- Envelope (shows after preloader) -->
    <Envelope v-if="showEnvelope" @opened="onEnvelopeOpened" />

    <!-- Audio Player (shows after envelope opens) -->
    <AudioPlayer v-if="showContent" />

    <!-- Main Content -->
    <transition name="content-fade">
      <main v-if="showContent" class="app__main">
        <div class="app__wrapper">
          <HeroSection />
          <Countdown />
          <!-- <SaveTheDate /> -->
          <PhotoGallery />
          <!-- <Agenda /> -->
          <VenueAndRules />
          <WishesWall />
          <!-- <RSVP /> -->

          <!-- Footer -->
          <footer class="app__footer">
            <div class="app__footer-inner">
              <p class="app__footer-names">Bahaa & Eman</p>
              <p class="app__footer-date">23 · 10 · 2026</p>
              <div class="app__footer-line"></div>
              <p class="app__footer-note">Made with love</p>
            </div>
          </footer>
        </div>
      </main>
    </transition>

    <!-- Background pattern for desktop -->
    <div class="app__desktop-bg" aria-hidden="true"></div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Preloader from '@/components/Preloader.vue'
import Envelope from '@/components/Envelope.vue'
import AudioPlayer from '@/components/AudioPlayer.vue'
import HeroSection from '@/components/HeroSection.vue'
import Countdown from '@/components/Countdown.vue'
// import SaveTheDate from '@/components/SaveTheDate.vue'
import PhotoGallery from '@/components/PhotoGallery.vue'
// import Agenda from '@/components/Agenda.vue'
import VenueAndRules from '@/components/VenueAndRules.vue'
import WishesWall from '@/components/WishesWall.vue'
// import RSVP from '@/components/RSVP.vue'

const showPreloader = ref(true)
const showEnvelope = ref(false)
const showContent = ref(false)

function onPreloaderDone() {
  showPreloader.value = false
  showEnvelope.value = true
}

function onEnvelopeOpened() {
  showEnvelope.value = false
  showContent.value = true
}
</script>

<style scoped>
.app {
  position: relative;
  min-height: 100vh;
  min-height: 100dvh;
}

/* Desktop background pattern */
.app__desktop-bg {
  display: none;
}

@media (min-width: 480px) {
  .app__desktop-bg {
    display: block;
    position: fixed;
    inset: 0;
    z-index: -1;
    background-color: var(--color-navy);
    background-image:
      radial-gradient(circle at 20% 50%, rgba(196, 164, 155, 0.08) 0%, transparent 50%),
      radial-gradient(circle at 80% 50%, rgba(196, 164, 155, 0.08) 0%, transparent 50%);
  }
}

/* Main content wrapper — mobile-first centered */
.app__wrapper {
  max-width: 28rem; /* max-w-md equivalent */
  margin: 0 auto;
  position: relative;
  background: var(--color-ivory);
  min-height: 100vh;
  min-height: 100dvh;
}

@media (min-width: 480px) {
  .app__wrapper {
    box-shadow: 0 0 60px rgba(0, 0, 0, 0.3);
  }
}

/* Content fade-in transition */
.content-fade-enter-active {
  transition: opacity 0.8s ease;
}
.content-fade-enter-from {
  opacity: 0;
}

/* Footer */
.app__footer {
  padding: 3rem 1.5rem;
  background: var(--color-ivory-dark);
  text-align: center;
}

.app__footer-inner {
  max-width: 400px;
  margin: 0 auto;
}

.app__footer-names {
  font-family: var(--font-cursive);
  font-size: 2rem;
  color: var(--color-navy);
}

.app__footer-date {
  font-family: var(--font-serif);
  font-size: 0.85rem;
  color: var(--color-navy-light);
  letter-spacing: 0.15em;
  margin-top: 0.5rem;
}

.app__footer-line {
  width: 40px;
  height: 1px;
  background: var(--color-gold);
  margin: 1.5rem auto;
  opacity: 0.5;
}

.app__footer-note {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  opacity: 0.5;
}
</style>
