<template>
  <div v-if="!dismissed" class="envelope-screen" :class="{ 'envelope-screen--fading': isFading }">
    <!-- Floating sparkles across the screen -->
    <div class="envelope-screen__particles">
      <span v-for="n in 18" :key="n" class="particle" :style="particleStyle(n)">✦</span>
    </div>

    <!-- Top label -->
    <p class="envelope-screen__pretext" :class="{ 'animate-in': showElements }">
      You Have Received An Invitation
    </p>

    <!-- ═══ ENVELOPE ═══ -->
    <div class="envelope" :class="{ 'envelope--opened': isOpened }">

      <!-- BODY (cream rectangle) -->
      <div class="envelope__body"></div>

      <!-- Left fold triangle -->
      <div class="envelope__fold-left"></div>
      <!-- Right fold triangle (mirror of left) -->
      <div class="envelope__fold-right"></div>

      <!-- BOTTOM FLAP -->
      <div class="envelope__bottom-flap"></div>

      <!-- TOP FLAP (rotates open) -->
      <div class="envelope__flap" :class="{ 'envelope__flap--open': isOpened }"></div>

      <!-- Gold shimmer overlay on the envelope -->
      <div class="envelope__shimmer"></div>

      <!-- Sparkle dots on the envelope -->
      <div class="envelope__sparkles">
        <span v-for="s in 12" :key="'s'+s" class="sparkle-dot" :style="sparkleStyle(s)"></span>
      </div>

      <!-- INNER CARD -->
      <div class="envelope__card" :class="{ 'envelope__card--revealed': isOpened }">
        <div class="envelope__card-inner">
          <img :src="floralFrame" alt="" class="envelope__card-frame" />
          <div class="envelope__card-content">
            <p class="envelope__card-eyebrow">You Are Cordially Invited</p>
            <p class="envelope__card-subline">to the engagement of</p>
            <h2 class="envelope__card-names">Bahaa &amp; Eman</h2>
            <div class="envelope__card-divider">
              <span class="div-line"></span>
              <span class="div-gem">◆</span>
              <span class="div-line"></span>
            </div>
            <p class="envelope__card-date">23 · 10 · 2026</p>
            <p class="envelope__card-day">Friday Evening</p>
          </div>
        </div>
      </div>
    </div>

    <!-- WAX SEAL -->
    <button
      v-if="!isOpened"
      class="envelope-screen__seal"
      :class="{ 'animate-in': showElements }"
      @click="openEnvelope"
      aria-label="Open invitation"
    >
      <div class="seal__ring"></div>
      <span class="seal__monogram">B &amp; E</span>
      <span class="seal__text">Open</span>
    </button>

    <p v-if="!isOpened" class="envelope-screen__hint" :class="{ 'animate-in': showElements }">
      Tap the seal to open
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import floralFrame from '@/assets/images/floral-frame.png'

const emit = defineEmits(['opened'])
const isOpened = ref(false)
const isFading = ref(false)
const dismissed = ref(false)
const showElements = ref(false)

onMounted(() => {
  setTimeout(() => {
    showElements.value = true
  }, 300)
})

function particleStyle(n) {
  const x = Math.random() * 100
  const y = Math.random() * 100
  const size = 8 + Math.random() * 10
  const delay = Math.random() * 6
  const duration = 4 + Math.random() * 5
  return {
    left: `${x}%`,
    top: `${y}%`,
    fontSize: `${size}px`,
    animationDelay: `${delay}s`,
    animationDuration: `${duration}s`,
  }
}

function sparkleStyle(s) {
  // Distribute sparkles evenly across the envelope surface
  const x = 10 + Math.random() * 80
  const y = 10 + Math.random() * 80
  const size = 3 + Math.random() * 5
  const delay = Math.random() * 3
  return {
    left: `${x}%`,
    top: `${y}%`,
    width: `${size}px`,
    height: `${size}px`,
    animationDelay: `${delay}s`,
  }
}

function openEnvelope() {
  isOpened.value = true
  setTimeout(() => {
    isFading.value = true
    setTimeout(() => {
      emit('opened')
      dismissed.value = true
    }, 800)
  }, 2500)
}
</script>

<style scoped>
/* ── Screen ── */
.envelope-screen {
  position: fixed;
  inset: 0;
  z-index: 500;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2.5rem;
  background:
    radial-gradient(ellipse at 25% 20%, rgba(216, 200, 184, 0.45) 0%, transparent 55%),
    radial-gradient(ellipse at 75% 80%, rgba(239, 231, 220, 0.55) 0%, transparent 55%),
    linear-gradient(160deg, #f9f6f0 0%, #f4efea 50%, #efe7dc 100%);
  overflow: hidden;
  transition: opacity 0.8s ease;
}
.envelope-screen--fading {
  opacity: 0;
  pointer-events: none;
}

/* ── Floating sparkles ── */
.envelope-screen__particles {
  position: absolute;
  inset: 0;
  pointer-events: none;
}
.particle {
  position: absolute;
  color: rgba(196, 164, 155, 0.55);
  animation: particleFloat var(--duration, 5s) ease-in-out infinite alternate;
  user-select: none;
}
@keyframes particleFloat {
  0%   { opacity: 0;   transform: translateY(0px) rotate(0deg) scale(0.5); }
  50%  { opacity: 0.8; }
  100% { opacity: 0;   transform: translateY(-50px) rotate(30deg) scale(1.2); }
}

/* ── Top label ── */
.envelope-screen__pretext {
  font-family: var(--font-sans);
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.4em;
  text-transform: uppercase;
  color: var(--color-navy);
  opacity: 0;
  transform: translateY(10px);
  transition: all 0.8s ease 0.2s;
  text-align: center;
}
.envelope-screen__pretext.animate-in {
  opacity: 0.85;
  transform: translateY(0);
}

/* ══════════════════════════════════
   ENVELOPE (Burgundy Theme)
   ══════════════════════════════════ */
.envelope {
  position: relative;
  width: 300px;
  height: 220px;
  perspective: 1200px;
  filter: drop-shadow(0 25px 50px rgba(74, 20, 26, 0.35)) drop-shadow(0 8px 16px rgba(0, 0, 0, 0.18));
}

/* ── Body (Burgundy rectangle) ── */
.envelope__body {
  position: absolute;
  inset: 0;
  border-radius: 8px;
  background: linear-gradient(165deg, #5c1d24 0%, #4a141a 60%, #380d13 100%);
  border: 1.5px solid rgba(196, 164, 155, 0.45);
}
/* Inner border */
.envelope__body::after {
  content: '';
  position: absolute;
  inset: 6px;
  border: 1px solid rgba(216, 200, 184, 0.22);
  border-radius: 4px;
  pointer-events: none;
}

/* ── Fold triangles (LEFT & RIGHT — Burgundy tones) ── */
.envelope__fold-left,
.envelope__fold-right {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 50%;
  overflow: hidden;
  z-index: 2;
}
.envelope__fold-left {
  left: 0;
}
.envelope__fold-right {
  right: 0;
}
/* Left triangle */
.envelope__fold-left::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(74, 20, 26, 0.85), rgba(46, 11, 15, 0.95));
  clip-path: polygon(0 0, 100% 50%, 0 100%);
}
/* Right triangle */
.envelope__fold-right::before {
  content: '';
  position: absolute;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(225deg, rgba(74, 20, 26, 0.85), rgba(46, 11, 15, 0.95));
  clip-path: polygon(100% 0, 0 50%, 100% 100%);
}

/* ── TOP FLAP (Burgundy triangle pointing down) ── */
.envelope__flap {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 0;
  border-left: 150px solid transparent;
  border-right: 150px solid transparent;
  border-top: 115px solid #5c1d24;
  z-index: 20;
  transform-origin: top center;
  transform-style: preserve-3d;
  transition: transform 1.1s cubic-bezier(0.4, 0, 0.2, 1);
  filter: drop-shadow(0 6px 12px rgba(0, 0, 0, 0.3));
}
/* Subtle sheen on flap */
.envelope__flap::before {
  content: '';
  position: absolute;
  top: -115px;
  left: -150px;
  right: -150px;
  height: 115px;
  background: linear-gradient(to bottom, rgba(216, 200, 184, 0.25), transparent);
  clip-path: polygon(0 0, 100% 0, 50% 100%);
  pointer-events: none;
}
.envelope__flap--open {
  transform: rotateX(-180deg);
}

/* ── BOTTOM FLAP (Burgundy triangle pointing up) ── */
.envelope__bottom-flap {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 0;
  border-left: 150px solid transparent;
  border-right: 150px solid transparent;
  border-bottom: 105px solid #461318;
  z-index: 8;
}

/* ── SHIMMER — sweeping light across the envelope ── */
.envelope__shimmer {
  position: absolute;
  inset: 0;
  z-index: 15;
  pointer-events: none;
  overflow: hidden;
  border-radius: 8px;
}
.envelope__shimmer::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -100%;
  width: 60%;
  height: 200%;
  background: linear-gradient(
    105deg,
    transparent 30%,
    rgba(216, 200, 184, 0.2) 45%,
    rgba(255, 255, 255, 0.35) 50%,
    rgba(216, 200, 184, 0.2) 55%,
    transparent 70%
  );
  animation: shimmerSweep 4s ease-in-out infinite;
}
@keyframes shimmerSweep {
  0%   { left: -100%; }
  100% { left: 200%; }
}

/* ── SPARKLE DOTS — small glowing dots that twinkle ── */
.envelope__sparkles {
  position: absolute;
  inset: 0;
  z-index: 16;
  pointer-events: none;
}
.sparkle-dot {
  position: absolute;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(216, 200, 184, 0.95), rgba(216, 200, 184, 0) 70%);
  animation: twinkle 2s ease-in-out infinite;
}
@keyframes twinkle {
  0%, 100% { opacity: 0; transform: scale(0.3); }
  50%      { opacity: 1; transform: scale(1); }
}

/* ── INNER CARD (Ivory contrast card) ── */
.envelope__card {
  position: absolute;
  top: 10px;
  left: 16px;
  right: 16px;
  bottom: 10px;
  z-index: 5;
  transform: translateY(15px) scale(0.88);
  opacity: 0;
  transition:
    transform 1.5s cubic-bezier(0.34, 1.56, 0.64, 1) 0.9s,
    opacity 0.7s ease 0.9s;
}
.envelope__card--revealed {
  transform: translateY(-160px) scale(1.05);
  opacity: 1;
  z-index: 30;
}

.envelope__card-inner {
  width: 100%;
  height: 100%;
  background: linear-gradient(170deg, #f9f6f0 0%, #f4efea 60%, #efe7dc 100%);
  border-radius: 8px;
  border: 1.5px solid rgba(196, 164, 155, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  box-shadow:
    0 16px 45px rgba(0, 0, 0, 0.35),
    0 4px 12px rgba(74, 20, 26, 0.2),
    inset 0 0 0 1px rgba(255,255,255,0.8);
}

.envelope__card-frame {
  position: absolute;
  inset: 4px;
  width: calc(100% - 8px);
  height: calc(100% - 8px);
  object-fit: contain;
  opacity: 0.35;
  pointer-events: none;
}

.envelope__card-content {
  text-align: center;
  position: relative;
  z-index: 2;
  padding: 0.5rem;
}

.envelope__card-eyebrow {
  font-family: var(--font-sans);
  font-size: 0.5rem;
  letter-spacing: 0.4em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.35rem;
}
.envelope__card-subline {
  font-family: var(--font-serif);
  font-size: 0.7rem;
  font-style: italic;
  color: var(--color-navy-light);
  margin-bottom: 0.5rem;
}
.envelope__card-names {
  font-family: var(--font-cursive);
  font-size: 2rem;
  color: var(--color-navy);
  line-height: 1.2;
  margin-bottom: 0.5rem;
  text-shadow: 0 1px 2px rgba(74, 20, 26, 0.1);
}
.envelope__card-divider {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.4rem;
  margin-bottom: 0.5rem;
}
.div-line {
  width: 30px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}
.div-gem {
  font-size: 0.4rem;
  color: var(--color-gold);
}
.envelope__card-date {
  font-family: var(--font-serif);
  font-size: 0.85rem;
  color: var(--color-navy);
  letter-spacing: 0.15em;
}
.envelope__card-day {
  font-family: var(--font-sans);
  font-size: 0.55rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-top: 0.25rem;
}

/* ── WAX SEAL ── */
.envelope-screen__seal {
  position: relative;
  z-index: 100;
  width: 76px;
  height: 76px;
  border-radius: 50%;
  border: 1.5px solid rgba(216, 200, 184, 0.5);
  background: radial-gradient(ellipse at 35% 30%,
    #8c2732 0%,
    #5c1d24 45%,
    #4a141a 75%,
    #2c080e 100%
  );
  cursor: pointer;
  box-shadow:
    0 6px 25px rgba(0, 0, 0, 0.35),
    0 2px 10px rgba(74, 20, 26, 0.5),
    inset 0 -3px 5px rgba(0, 0, 0, 0.3),
    inset 0 3px 5px rgba(255, 255, 255, 0.35);
  opacity: 0;
  transform: translateY(10px) scale(0.9);
  transition: opacity 0.8s ease 0.6s, transform 0.8s ease 0.6s, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2px;
  margin-top: -0.5rem;
}
.envelope-screen__seal.animate-in {
  opacity: 1;
  transform: translateY(0) scale(1);
}
.envelope-screen__seal:hover {
  transform: scale(1.1) !important;
  box-shadow:
    0 8px 30px rgba(0, 0, 0, 0.45),
    0 4px 15px rgba(74, 20, 26, 0.7),
    inset 0 -3px 5px rgba(0, 0, 0, 0.3),
    inset 0 3px 5px rgba(255, 255, 255, 0.35);
}
.seal__ring {
  position: absolute;
  inset: 6px;
  border-radius: 50%;
  border: 1.5px solid rgba(216, 200, 184, 0.4);
  pointer-events: none;
}
.seal__monogram {
  font-family: var(--font-cursive);
  font-size: 1.15rem;
  font-weight: 500;
  color: var(--color-gold-light);
  line-height: 1;
  margin-top: -2px;
}
.seal__text {
  font-family: var(--font-serif);
  font-size: 0.6rem;
  font-weight: 600;
  color: #ffffff;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

/* ── Hint ── */
.envelope-screen__hint {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  opacity: 0;
  transform: translateY(5px);
  transition: all 0.6s ease 1s;
}
.envelope-screen__hint.animate-in {
  opacity: 1;
  transform: translateY(0);
}
.envelope-screen__hint.animate-in {
  opacity: 1;
  transform: translateY(0);
}

/* ── Responsive ── */
@media (max-width: 360px) {
  .envelope { width: 260px; height: 190px; }
  .envelope__flap {
    border-left-width: 130px;
    border-right-width: 130px;
    border-top-width: 100px;
  }
  .envelope__flap::before {
    top: -100px;
    left: -130px;
    right: -130px;
    height: 100px;
  }
  .envelope__bottom-flap {
    border-left-width: 130px;
    border-right-width: 130px;
    border-bottom-width: 92px;
  }
  .envelope__card-names { font-size: 1.7rem; }
}
</style>
