<template>
  <transition name="preloader-fade">
    <div v-if="visible" class="preloader">
      <!-- Decorative corner ornaments -->
      <div class="preloader__corner preloader__corner--tl"></div>
      <div class="preloader__corner preloader__corner--tr"></div>
      <div class="preloader__corner preloader__corner--bl"></div>
      <div class="preloader__corner preloader__corner--br"></div>

      <div class="preloader__content">
        <div class="preloader__initials">
          <span class="preloader__letter preloader__letter--first">B</span>
          <span class="preloader__ampersand">
            <svg viewBox="0 0 24 24" width="20" height="20" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>
            </svg>
          </span>
          <span class="preloader__letter preloader__letter--second">E</span>
        </div>
        <div class="preloader__ornament">
          <span class="preloader__orn-line"></span>
          <span class="preloader__orn-dot">◆</span>
          <span class="preloader__orn-line"></span>
        </div>
        <p class="preloader__tagline">We invite you to celebrate with us</p>
        <div class="preloader__loading">
          <div class="preloader__loading-bar"></div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['loaded'])
const visible = ref(true)

onMounted(() => {
  const minDelay = new Promise(resolve => setTimeout(resolve, 3000))
  const assetsReady = new Promise(resolve => {
    if (document.readyState === 'complete') {
      resolve()
    } else {
      window.addEventListener('load', resolve, { once: true })
    }
  })

  Promise.all([minDelay, assetsReady]).then(() => {
    visible.value = false
    setTimeout(() => emit('loaded'), 700)
  })
})
</script>

<style scoped>
.preloader {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(160deg, var(--color-warm-gray), var(--color-warm-gray-dark), var(--color-ivory));
  overflow: hidden;
}

/* Corner ornaments */
.preloader__corner {
  position: absolute;
  width: 60px;
  height: 60px;
  border-color: rgba(196, 164, 155, 0.4);
  border-style: solid;
}

.preloader__corner--tl { top: 24px; left: 24px; border-width: 1px 0 0 1px; }
.preloader__corner--tr { top: 24px; right: 24px; border-width: 1px 1px 0 0; }
.preloader__corner--bl { bottom: 24px; left: 24px; border-width: 0 0 1px 1px; }
.preloader__corner--br { bottom: 24px; right: 24px; border-width: 0 1px 1px 0; }

.preloader__content {
  text-align: center;
}

.preloader__initials {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  animation: fadeIn 1s ease forwards;
}

.preloader__letter {
  font-family: var(--font-serif);
  font-size: 4.5rem;
  font-weight: 600;
  color: var(--color-navy);
  letter-spacing: 0.05em;
  text-shadow: 0 2px 20px rgba(74, 20, 26, 0.08);
}

.preloader__letter--first {
  animation: fadeInUp 0.8s ease forwards;
  animation-delay: 0.3s;
  opacity: 0;
}

.preloader__letter--second {
  animation: fadeInUp 0.8s ease forwards;
  animation-delay: 0.6s;
  opacity: 0;
}

.preloader__ampersand {
  color: var(--color-gold);
  animation: fadeInUp 0.8s ease forwards;
  animation-delay: 0.45s;
  opacity: 0;
  display: flex;
  animation-fill-mode: forwards;
}

.preloader__ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin: 1.25rem 0;
  animation: fadeIn 0.8s ease forwards;
  animation-delay: 0.9s;
  opacity: 0;
}

.preloader__orn-line {
  width: 40px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}

.preloader__orn-dot {
  font-size: 0.4rem;
  color: var(--color-gold);
}

.preloader__tagline {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.35em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  opacity: 0;
  animation: fadeIn 0.8s ease forwards;
  animation-delay: 1.2s;
}

/* Loading bar */
.preloader__loading {
  width: 120px;
  height: 1px;
  background: rgba(196, 164, 155, 0.3);
  margin: 2rem auto 0;
  border-radius: 2px;
  overflow: hidden;
  animation: fadeIn 0.6s ease forwards;
  animation-delay: 1.5s;
  opacity: 0;
}

.preloader__loading-bar {
  width: 0;
  height: 100%;
  background: linear-gradient(90deg, var(--color-navy-dark), var(--color-gold), var(--color-gold-light));
  border-radius: 2px;
  animation: loadProgress 2.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
  animation-delay: 0.5s;
}

@keyframes loadProgress {
  0% { width: 0; }
  30% { width: 35%; }
  60% { width: 65%; }
  90% { width: 90%; }
  100% { width: 100%; }
}

/* Transition */
.preloader-fade-leave-active {
  transition: opacity 0.7s ease;
}
.preloader-fade-leave-to {
  opacity: 0;
}
</style>
