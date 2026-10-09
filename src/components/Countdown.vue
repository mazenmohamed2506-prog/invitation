<template>
  <section class="countdown" id="countdown">
    <div class="countdown__inner">
      <p class="countdown__pre">We're counting down to</p>
      <h2 class="countdown__heading">Our Special Day</h2>

      <!-- Ornamental divider -->
      <div class="countdown__ornament">
        <span class="countdown__orn-line"></span>
        <svg class="countdown__orn-icon" viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="1.5">
          <path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>
        </svg>
        <span class="countdown__orn-line"></span>
      </div>

      <div class="countdown__timer">
        <div class="countdown__block">
          <div class="countdown__number-wrap">
            <span class="countdown__number">{{ days }}</span>
          </div>
          <span class="countdown__label">Days</span>
        </div>

        <span class="countdown__separator">·</span>

        <div class="countdown__block">
          <div class="countdown__number-wrap">
            <span class="countdown__number">{{ hours }}</span>
          </div>
          <span class="countdown__label">Hours</span>
        </div>

        <span class="countdown__separator">·</span>

        <div class="countdown__block">
          <div class="countdown__number-wrap">
            <span class="countdown__number">{{ minutes }}</span>
          </div>
          <span class="countdown__label">Minutes</span>
        </div>
      </div>

      <!-- <p class="countdown__date-label">Friday</p> -->

    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Target date: October 23, 2026 at 7:00 PM (19:00)
const targetDate = new Date(2026, 9, 23, 19, 0, 0).getTime()

const days = ref('00')
const hours = ref('00')
const minutes = ref('00')
let intervalId = null

function pad(n) {
  return String(n).padStart(2, '0')
}

function updateCountdown() {
  const now = Date.now()
  const diff = targetDate - now

  if (diff <= 0) {
    days.value = '00'
    hours.value = '00'
    minutes.value = '00'
    if (intervalId) clearInterval(intervalId)
    return
  }

  const d = Math.floor(diff / (1000 * 60 * 60 * 24))
  const h = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))

  days.value = pad(d)
  hours.value = pad(h)
  minutes.value = pad(m)
}

onMounted(() => {
  updateCountdown()
  intervalId = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<style scoped>
.countdown {
  background: linear-gradient(180deg, var(--color-ivory), var(--color-ivory-dark));
  padding: 4.5rem 1.5rem;
  position: relative;
}

.countdown__inner {
  text-align: center;
  max-width: 400px;
  margin: 0 auto;
}

.countdown__pre {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.35em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.5rem;
}

.countdown__heading {
  font-family: var(--font-serif);
  font-size: 1.85rem;
  font-weight: 500;
  color: var(--color-navy);
}

/* Ornament */
.countdown__ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  margin: 1.25rem 0 2.5rem;
}

.countdown__orn-line {
  width: 50px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}

.countdown__orn-icon {
  color: var(--color-gold);
  flex-shrink: 0;
}

/* Timer */
.countdown__timer {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.25rem;
}

.countdown__block {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.countdown__number-wrap {
  width: 75px;
  height: 85px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--color-ivory);
  border-radius: 12px;
  box-shadow:
    0 4px 20px rgba(74, 20, 26, 0.06),
    0 1px 3px rgba(74, 20, 26, 0.04);
  border: 1px solid rgba(196, 164, 155, 0.35);
  position: relative;
}

/* Subtle gold top accent */
.countdown__number-wrap::before {
  content: '';
  position: absolute;
  top: 0;
  left: 20%;
  right: 20%;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
  border-radius: 0 0 2px 2px;
}

.countdown__number {
  font-family: var(--font-serif);
  font-size: 2.5rem;
  font-weight: 600;
  color: var(--color-navy);
  line-height: 1;
}

.countdown__label {
  font-family: var(--font-sans);
  font-size: 0.55rem;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-top: 0.6rem;
}

.countdown__separator {
  font-size: 1.5rem;
  color: var(--color-gold);
  margin-top: -1.5rem;
}

.countdown__date-label {
  font-family: var(--font-serif);
  font-size: 1rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-top: 2.2rem;
  letter-spacing: 0.05em;
  opacity: 0.9;
}

.countdown__time-label-ar {
  font-family: var(--font-sans);
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--color-gold-dark);
  margin-top: 0.35rem;
  letter-spacing: 0.04em;
}
</style>
