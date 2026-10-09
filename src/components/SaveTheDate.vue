<template>
  <section class="save-the-date" id="save-the-date">
    <div class="save-the-date__inner">
      <!-- Section Header -->
      <div class="save-the-date__header">
        <span class="save-the-date__eyebrow">Mark Your Calendar</span>
        <h2 class="save-the-date__title">Save the Date</h2>
        
        <svg class="save-the-date__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
          <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
          <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
          <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        </svg>
      </div>

      <!-- Luxury Burgundy Calendar Card -->
      <div class="calendar-card">
        <!-- Card Inner Border Accent -->
        <div class="calendar-card__border"></div>

        <!-- Month & Year Title with Floral motif -->
        <div class="calendar__header">
          <div class="calendar__floral-icon">
            <svg viewBox="0 0 24 24" width="22" height="22" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M12 21a9 9 0 0 0 9-9c0-4.97-4.03-9-9-9s-9 4.03-9 9a9 9 0 0 0 9 9z" stroke-opacity="0.3"/>
              <path d="M12 7c-2 2-2 5 0 7 2-2 2-5 0-7z"/>
              <path d="M7 12c2-2 5-2 7 0-2 2-5 2-7 0z"/>
            </svg>
          </div>
          <h3 class="calendar__month">October 2026</h3>
        </div>

        <!-- Divider Line -->
        <div class="calendar__line"></div>

        <!-- Weekday Headers -->
        <div class="calendar__weekdays">
          <span v-for="day in weekdays" :key="day" class="calendar__weekday">{{ day }}</span>
        </div>

        <!-- Days Grid -->
        <div class="calendar__grid">
          <!-- Empty slots for Monday–Wednesday (Oct 1 starts on Thursday) -->
          <div v-for="e in 3" :key="'empty-' + e" class="calendar__day calendar__day--empty"></div>

          <!-- Days 1 to 31 -->
          <div
            v-for="d in 31"
            :key="d"
            class="calendar__day"
            :class="{ 'calendar__day--wedding': d === 23 }"
          >
            <!-- Creamy Heart for wedding day (Oct 23) -->
            <div v-if="d === 23" class="calendar__heart-wrap">
              <svg class="calendar__heart-svg" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
              </svg>
              <span class="calendar__heart-text">23</span>
            </div>

            <!-- Normal Days -->
            <span v-else class="calendar__day-number">{{ d }}</span>
          </div>
        </div>

        <!-- Footer Date Callout -->
        <div class="calendar__footer">
          <div class="calendar__footer-gem">◆</div>
          <p class="calendar__footer-date">Friday, October 23, 2026</p>
          <p class="calendar__footer-tag">CICADA HALL · ARMED FORCES CLUB, ZAMALEK</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const weekdays = ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su']
</script>

<style scoped>
.save-the-date {
  padding: 4.5rem 1.25rem;
  background: var(--color-warm-gray);
  position: relative;
}

.save-the-date__inner {
  max-width: 420px;
  margin: 0 auto;
}

.save-the-date__header {
  text-align: center;
  margin-bottom: 2rem;
}

.save-the-date__eyebrow {
  display: block;
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.35rem;
  font-weight: 500;
}

.save-the-date__title {
  font-family: var(--font-serif);
  font-size: 1.85rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-bottom: 0.6rem;
}

.save-the-date__divider {
  display: block;
  width: 140px;
  height: 18px;
  margin: 0 auto;
  color: var(--color-gold);
}

/* ── Luxury Burgundy Calendar Card ── */
.calendar-card {
  position: relative;
  background: linear-gradient(165deg, #5c1d24 0%, #4a141a 60%, #340c11 100%);
  border-radius: 16px;
  padding: 2.25rem 1.75rem 2rem;
  text-align: center;
  border: 1.5px solid rgba(216, 200, 184, 0.4);
  box-shadow:
    0 20px 45px rgba(74, 20, 26, 0.3),
    0 4px 15px rgba(0, 0, 0, 0.15);
  overflow: hidden;
}

/* Inner hairline frame */
.calendar-card__border {
  position: absolute;
  inset: 8px;
  border: 1px solid rgba(216, 200, 184, 0.2);
  border-radius: 10px;
  pointer-events: none;
}

/* Header */
.calendar__header {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  margin-bottom: 0.25rem;
}

.calendar__floral-icon {
  position: absolute;
  left: 0.25rem;
  top: 50%;
  transform: translateY(-50%);
  color: var(--color-gold-light);
  opacity: 0.75;
}

.calendar__month {
  font-family: var(--font-cursive);
  font-size: 2.6rem;
  font-weight: 400;
  color: #ffffff;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.4);
  line-height: 1.1;
}

/* Divider Line */
.calendar__line {
  width: 100%;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(216, 200, 184, 0.35) 15%,
    rgba(216, 200, 184, 0.85) 50%,
    rgba(216, 200, 184, 0.35) 85%,
    transparent
  );
  margin: 1rem 0 1.35rem;
}

/* Weekday row */
.calendar__weekdays {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 0.25rem;
  margin-bottom: 0.85rem;
}

.calendar__weekday {
  font-family: var(--font-sans);
  font-size: 0.72rem;
  font-weight: 600;
  color: var(--color-gold-light);
  letter-spacing: 0.05em;
  opacity: 0.9;
}

/* Days Grid */
.calendar__grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  row-gap: 0.85rem;
  column-gap: 0.25rem;
  align-items: center;
}

.calendar__day {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 34px;
}

.calendar__day--empty {
  visibility: hidden;
}

.calendar__day-number {
  font-family: var(--font-serif);
  font-size: 1rem;
  color: #f9f6f0;
  font-weight: 400;
  transition: transform 0.2s ease, color 0.2s ease;
}

.calendar__day:not(.calendar__day--wedding):hover .calendar__day-number {
  color: #ffffff;
  font-weight: 600;
  transform: scale(1.2);
  text-shadow: 0 0 8px rgba(255, 255, 255, 0.6);
}

/* Wedding Day Heart Badge (Cream/Ivory on Burgundy) */
.calendar__heart-wrap {
  position: relative;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: heartPulse 2.5s ease-in-out infinite;
}

.calendar__heart-svg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  color: #f4efea;
  filter: drop-shadow(0 4px 10px rgba(0, 0, 0, 0.4));
  transform: scale(1.18);
}

.calendar__heart-text {
  position: relative;
  z-index: 2;
  font-family: var(--font-serif);
  font-size: 0.88rem;
  font-weight: 800;
  color: var(--color-navy);
  margin-top: -2px;
}

@keyframes heartPulse {
  0%, 100% { transform: scale(1); }
  50%      { transform: scale(1.1); }
}

/* Calendar Footer */
.calendar__footer {
  margin-top: 1.75rem;
  padding-top: 1.25rem;
  border-top: 1px dashed rgba(216, 200, 184, 0.35);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.35rem;
}

.calendar__footer-gem {
  font-size: 0.45rem;
  color: var(--color-gold-light);
  margin-bottom: 0.15rem;
}

.calendar__footer-date {
  font-family: var(--font-serif);
  font-size: 1.05rem;
  font-weight: 500;
  color: #ffffff;
  letter-spacing: 0.05em;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
}

.calendar__footer-tag {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  opacity: 0.9;
}
</style>
