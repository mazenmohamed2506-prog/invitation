<template>
  <section class="gallery-section" id="gallery">
    <div class="gallery-section__inner">
      <!-- Section Header -->
      <div class="gallery-section__header">
        <span class="gallery-section__eyebrow">Captured Moments · لحظات لا تُنسى</span>
        <h2 class="gallery-section__title">Our Moments of Love</h2>

        <svg class="gallery-section__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
          <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
          <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
          <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        </svg>
      </div>

      <!-- Main Showcase Card with 3D Tilt & Glassmorphism -->
      <div class="gallery-card" @mouseenter="pauseAutoplay" @mouseleave="startAutoplay">
        <!-- Floating sparkle particles -->
        <div class="gallery-card__sparkles">
          <span v-for="n in 6" :key="n" class="card-sparkle" :style="sparkleStyle(n)">✦</span>
        </div>

        <!-- Main Photo Stage with Smooth Transitions -->
        <div class="gallery-card__stage" @click="openLightbox(currentIndex)">
          <transition name="photo-fade" mode="out-in">
            <div :key="currentIndex" class="gallery-card__image-wrap">
              <img
                :src="photos[currentIndex].src"
                :alt="photos[currentIndex].title"
                class="gallery-card__image"
              />
              <div class="gallery-card__overlay">
                <span class="gallery-card__badge">{{ photos[currentIndex].tag }}</span>
                <div class="gallery-card__text-block">
                  <h3 class="gallery-card__photo-title">{{ photos[currentIndex].title }}</h3>
                  <p class="gallery-card__photo-caption">{{ photos[currentIndex].caption }}</p>
                </div>
                <div class="gallery-card__zoom-hint">
                  <svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="currentColor" stroke-width="2">
                    <circle cx="11" cy="11" r="8"></circle>
                    <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
                    <line x1="11" y1="8" x2="11" y2="14"></line>
                    <line x1="8" y1="11" x2="14" y2="11"></line>
                  </svg>
                  <span>Tap to view full</span>
                </div>
              </div>
            </div>
          </transition>

          <!-- Navigation Arrow Buttons -->
          <button
            class="gallery-nav-btn gallery-nav-btn--prev"
            @click.stop="prevPhoto"
            aria-label="Previous photo"
          >
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="15 18 9 12 15 6"></polyline>
            </svg>
          </button>

          <button
            class="gallery-nav-btn gallery-nav-btn--next"
            @click.stop="nextPhoto"
            aria-label="Next photo"
          >
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="9 18 15 12 9 6"></polyline>
            </svg>
          </button>
        </div>

        <!-- Autoplay Progress Indicator -->
        <div class="gallery-card__progress">
          <div class="gallery-card__progress-bar" :style="{ width: progressPercent + '%' }"></div>
        </div>

        <!-- Thumbnails Strip -->
        <div class="gallery-thumbs">
          <button
            v-for="(photo, idx) in photos"
            :key="idx"
            class="gallery-thumb"
            :class="{ 'gallery-thumb--active': currentIndex === idx }"
            @click="selectPhoto(idx)"
            :aria-label="'View ' + photo.title"
          >
            <img :src="photo.src" :alt="photo.title" class="gallery-thumb__img" />
            <span class="gallery-thumb__indicator"></span>
          </button>
        </div>
      </div>
    </div>

    <!-- Fullscreen Romantic Lightbox Modal -->
    <transition name="lightbox-fade">
      <div v-if="lightboxOpen" class="lightbox" @click="closeLightbox">
        <div class="lightbox__backdrop"></div>
        <button class="lightbox__close" @click="closeLightbox" aria-label="Close modal">
          <svg viewBox="0 0 24 24" width="22" height="22" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>

        <div class="lightbox__content" @click.stop>
          <img :src="photos[currentIndex].src" :alt="photos[currentIndex].title" class="lightbox__img" />
          <div class="lightbox__info">
            <span class="lightbox__tag">{{ photos[currentIndex].tag }}</span>
            <h3 class="lightbox__title">{{ photos[currentIndex].title }}</h3>
            <p class="lightbox__caption">{{ photos[currentIndex].caption }}</p>
          </div>
        </div>
      </div>
    </transition>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

import deblaImg from '@/assets/images/debla.jpg'
import handImg from '@/assets/images/hand.jpg'
import hand1Img from '@/assets/images/hand1.jpg'
import personImg from '@/assets/images/person.jpg'

const photos = [
  {
    src: deblaImg,
    tag: 'The Rings · دبلة الخطوبة',
    title: 'The Eternal Promise',
    caption: 'With this ring, our forever begins — رمز المحبة والعهد الأبدي',
  },
  {
    src: handImg,
    tag: 'Together · يداً بيد',
    title: 'Walking Hand in Hand',
    caption: 'Two souls joined on a journey of a lifetime — خطوة بخطوة نحو الغد',
  },
  {
    src: hand1Img,
    tag: 'Harmony · قلوب مؤتلفة',
    title: 'A Touch of Grace',
    caption: 'Every beat of our hearts tells our story — أجمل الحكايات تُروى معاً',
  },
  {
    src: personImg,
    tag: 'Cherished · نظرة من القلب',
    title: 'In Your Eyes, Home',
    caption: 'Pure warmth, boundless smiles, and shared joy — الفرحة تكتمل بكم',
  },
]

const currentIndex = ref(0)
const lightboxOpen = ref(false)
const progressPercent = ref(0)

let timer = null
let progressInterval = null
const SLIDE_DURATION = 4500

function startAutoplay() {
  stopAutoplay()
  progressPercent.value = 0
  const stepTime = 50
  const increment = (stepTime / SLIDE_DURATION) * 100

  progressInterval = setInterval(() => {
    progressPercent.value += increment
    if (progressPercent.value >= 100) {
      progressPercent.value = 0
      nextPhoto()
    }
  }, stepTime)
}

function stopAutoplay() {
  if (progressInterval) {
    clearInterval(progressInterval)
    progressInterval = null
  }
}

function pauseAutoplay() {
  stopAutoplay()
}

function selectPhoto(index) {
  currentIndex.value = index
  startAutoplay()
}

function nextPhoto() {
  currentIndex.value = (currentIndex.value + 1) % photos.length
  progressPercent.value = 0
}

function prevPhoto() {
  currentIndex.value = (currentIndex.value - 1 + photos.length) % photos.length
  progressPercent.value = 0
}

function openLightbox(index) {
  currentIndex.value = index
  lightboxOpen.value = true
  stopAutoplay()
}

function closeLightbox() {
  lightboxOpen.value = false
  startAutoplay()
}

function sparkleStyle(n) {
  const left = (n * 16) + '%'
  const top = (n % 2 === 0 ? 10 : 85) + '%'
  const delay = (n * 0.4) + 's'
  return {
    left,
    top,
    animationDelay: delay,
  }
}

onMounted(() => {
  startAutoplay()
})

onUnmounted(() => {
  stopAutoplay()
})
</script>

<style scoped>
.gallery-section {
  padding: 4.5rem 1.25rem;
  background: var(--color-warm-gray);
  position: relative;
  overflow: hidden;
}

.gallery-section__inner {
  max-width: 420px;
  margin: 0 auto;
}

.gallery-section__header {
  text-align: center;
  margin-bottom: 2rem;
}

.gallery-section__eyebrow {
  display: block;
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.35rem;
  font-weight: 600;
}

.gallery-section__title {
  font-family: var(--font-serif);
  font-size: 1.85rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-bottom: 0.6rem;
  letter-spacing: 0.02em;
}

.gallery-section__divider {
  display: block;
  width: 140px;
  height: 18px;
  margin: 0 auto;
  color: var(--color-gold);
}

/* ── Main Showcase Card ── */
.gallery-card {
  position: relative;
  background: linear-gradient(165deg, #5c1d24 0%, #4a141a 60%, #340c11 100%);
  border-radius: 18px;
  padding: 1.25rem 1rem 1.25rem;
  box-shadow:
    0 22px 50px rgba(74, 20, 26, 0.32),
    0 4px 18px rgba(0, 0, 0, 0.16);
  border: 1.5px solid rgba(216, 200, 184, 0.45);
  overflow: hidden;
}

/* Floating Sparkles */
.gallery-card__sparkles {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 1;
}

.card-sparkle {
  position: absolute;
  color: rgba(216, 200, 184, 0.6);
  font-size: 0.75rem;
  animation: sparkleTwinkle 2.8s infinite ease-in-out alternate;
}

@keyframes sparkleTwinkle {
  0%   { opacity: 0.2; transform: scale(0.6) rotate(0deg); }
  50%  { opacity: 0.9; transform: scale(1.1) rotate(45deg); }
  100% { opacity: 0.3; transform: scale(0.7) rotate(90deg); }
}

/* Photo Stage */
.gallery-card__stage {
  position: relative;
  width: 100%;
  aspect-ratio: 4 / 4.6;
  border-radius: 14px;
  overflow: hidden;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.35);
  border: 1.5px solid rgba(216, 200, 184, 0.35);
  cursor: pointer;
  background: #2a090e;
}

.gallery-card__image-wrap {
  position: relative;
  width: 100%;
  height: 100%;
}

.gallery-card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.gallery-card__stage:hover .gallery-card__image {
  transform: scale(1.05);
}

/* Luminous Overlay */
.gallery-card__overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 1rem 1.15rem;
  background: linear-gradient(
    to bottom,
    rgba(30, 6, 9, 0.45) 0%,
    transparent 35%,
    rgba(25, 4, 8, 0.88) 85%,
    rgba(15, 2, 5, 0.96) 100%
  );
  z-index: 2;
  pointer-events: none;
}

.gallery-card__badge {
  align-self: flex-start;
  font-family: var(--font-sans);
  font-size: 0.58rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: #ffffff;
  background: rgba(74, 20, 26, 0.85);
  backdrop-filter: blur(8px);
  padding: 0.28rem 0.65rem;
  border-radius: 14px;
  border: 1px solid rgba(216, 200, 184, 0.5);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
}

.gallery-card__text-block {
  text-align: left;
  margin-top: auto;
}

.gallery-card__photo-title {
  font-family: var(--font-serif);
  font-size: 1.35rem;
  font-weight: 600;
  color: #ffffff;
  line-height: 1.25;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
  margin-bottom: 0.25rem;
}

.gallery-card__photo-caption {
  font-family: var(--font-sans);
  font-size: 0.72rem;
  color: var(--color-gold-light);
  line-height: 1.45;
  text-shadow: 0 1px 4px rgba(0, 0, 0, 0.6);
  opacity: 0.95;
}

.gallery-card__zoom-hint {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  font-family: var(--font-sans);
  font-size: 0.55rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  margin-top: 0.45rem;
  opacity: 0.8;
}

/* Nav Buttons */
.gallery-nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: rgba(46, 11, 15, 0.78);
  backdrop-filter: blur(6px);
  border: 1px solid rgba(216, 200, 184, 0.45);
  color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.25s ease;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.35);
}

.gallery-nav-btn:hover {
  background: rgba(92, 29, 36, 0.95);
  border-color: rgba(216, 200, 184, 0.9);
  transform: translateY(-50%) scale(1.1);
}

.gallery-nav-btn--prev {
  left: 10px;
}

.gallery-nav-btn--next {
  right: 10px;
}

/* Autoplay Progress Bar */
.gallery-card__progress {
  width: 100%;
  height: 2.5px;
  background: rgba(216, 200, 184, 0.2);
  border-radius: 2px;
  margin: 0.85rem 0 0.95rem;
  overflow: hidden;
}

.gallery-card__progress-bar {
  height: 100%;
  background: linear-gradient(90deg, var(--color-gold), var(--color-gold-light));
  transition: width 0.05s linear;
  border-radius: 2px;
}

/* Thumbnails Strip */
.gallery-thumbs {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.55rem;
  position: relative;
  z-index: 2;
}

.gallery-thumb {
  position: relative;
  aspect-ratio: 1;
  border-radius: 10px;
  overflow: hidden;
  border: 2px solid rgba(216, 200, 184, 0.3);
  padding: 0;
  background: transparent;
  cursor: pointer;
  transition: all 0.25s ease;
}

.gallery-thumb__img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  filter: brightness(0.75);
  transition: filter 0.25s ease;
}

.gallery-thumb:hover .gallery-thumb__img,
.gallery-thumb--active .gallery-thumb__img {
  filter: brightness(1);
}

.gallery-thumb--active {
  border-color: var(--color-gold-light);
  transform: translateY(-2px);
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.4);
}

.gallery-thumb__indicator {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--color-gold-light);
  opacity: 0;
  transition: opacity 0.25s ease;
}

.gallery-thumb--active .gallery-thumb__indicator {
  opacity: 1;
}

/* Lightbox Modal */
.lightbox {
  position: fixed;
  inset: 0;
  z-index: 10000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
}

.lightbox__backdrop {
  position: absolute;
  inset: 0;
  background: rgba(20, 4, 7, 0.92);
  backdrop-filter: blur(12px);
}

.lightbox__close {
  position: absolute;
  top: 1.25rem;
  right: 1.25rem;
  z-index: 10002;
  width: 42px;
  height: 42px;
  border-radius: 50%;
  background: rgba(74, 20, 26, 0.7);
  border: 1px solid rgba(216, 200, 184, 0.4);
  color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s ease;
}

.lightbox__close:hover {
  background: rgba(92, 29, 36, 0.95);
  transform: rotate(90deg);
}

.lightbox__content {
  position: relative;
  z-index: 10001;
  max-width: 440px;
  width: 100%;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6);
  border: 1.5px solid rgba(216, 200, 184, 0.5);
  background: #340c11;
}

.lightbox__img {
  width: 100%;
  max-height: 60vh;
  object-fit: contain;
  background: #180306;
  display: block;
}

.lightbox__info {
  padding: 1.15rem 1.25rem;
  background: linear-gradient(175deg, #4a141a, #2c080e);
  text-align: center;
}

.lightbox__tag {
  display: inline-block;
  font-family: var(--font-sans);
  font-size: 0.6rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  margin-bottom: 0.3rem;
}

.lightbox__title {
  font-family: var(--font-serif);
  font-size: 1.35rem;
  font-weight: 500;
  color: #ffffff;
  margin-bottom: 0.35rem;
}

.lightbox__caption {
  font-family: var(--font-sans);
  font-size: 0.75rem;
  color: var(--color-ivory);
  opacity: 0.85;
  line-height: 1.45;
}

/* Animations */
.photo-fade-enter-active,
.photo-fade-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.photo-fade-enter-from {
  opacity: 0;
  transform: scale(0.97);
}

.photo-fade-leave-to {
  opacity: 0;
  transform: scale(1.03);
}

.lightbox-fade-enter-active,
.lightbox-fade-leave-active {
  transition: opacity 0.35s ease;
}

.lightbox-fade-enter-from,
.lightbox-fade-leave-to {
  opacity: 0;
}
</style>
