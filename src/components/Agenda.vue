<template>
  <section class="agenda" id="agenda">
    <div class="agenda__inner">
      <div class="agenda__header">
        <span class="agenda__subheading">Engagement Schedule</span>
        <h2 class="agenda__heading">Order of the Day</h2>
        
        <svg class="agenda__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
          <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
          <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
          <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        </svg>
      </div>

      <div class="agenda__timeline">
        <!-- Connecting central vertical track -->
        <div class="agenda__track"></div>

        <div
          v-for="(event, index) in events"
          :key="index"
          ref="cardRefs"
          class="agenda__item"
          :class="{ 'agenda__item--visible': visibleCards[index] }"
        >
          <!-- Timeline Node Point -->
          <div class="agenda__node">
            <div class="agenda__node-dot"></div>
          </div>

          <!-- Event Card -->
          <div class="agenda__card">
            <div class="agenda__card-icon">
              <component :is="event.icon" />
            </div>

            <div class="agenda__card-content">
              <div class="agenda__card-header">
                <span class="agenda__card-time">{{ event.time }}</span>
                <span class="agenda__card-tag">{{ event.tag }}</span>
              </div>
              <h3 class="agenda__card-title">{{ event.title }}</h3>
              <p class="agenda__card-desc">{{ event.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, h } from 'vue'

// Custom Wedding-specific SVG Icons
const WelcomeIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M8 22h8' }),
    h('path', { d: 'M12 11v11' }),
    h('path', { d: 'M19.5 2L17 11H7L4.5 2' }),
    h('path', { d: 'M6 5h12' }),
  ])
}

const ZaffaIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M12 2l2.4 7.2h7.6l-6.1 4.5 2.3 7.3-6.2-4.6-6.2 4.6 2.3-7.3-6.1-4.5h7.6z' }),
  ])
}

const FirstDanceIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z' }),
    h('path', { d: 'M17 12l2 2 4-4' })
  ])
}

const CakeIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M20 21v-8a2 2 0 0 0-2-2H6a2 2 0 0 0-2 2v8' }),
    h('path', { d: 'M4 16s.5-1 2-1 2.5 2 4 2 2.5-2 4-2 2.5 2 4 2 2-1 2-1' }),
    h('path', { d: 'M2 21h20' }),
    h('path', { d: 'M7 8v3' }),
    h('path', { d: 'M12 8v3' }),
    h('path', { d: 'M17 8v3' }),
    h('circle', { cx: '12', cy: '4', r: '1.5' }),
  ])
}

const BanquetIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M18 8h1a4 4 0 0 1 0 8h-1' }),
    h('path', { d: 'M2 8h16v9a4 4 0 0 1-4 4H6a4 4 0 0 1-4-4V8z' }),
    h('line', { x1: '6', y1: '1', x2: '6', y2: '4' }),
    h('line', { x1: '10', y1: '1', x2: '10', y2: '4' }),
    h('line', { x1: '14', y1: '1', x2: '14', y2: '4' }),
  ])
}

const PhotoIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z' }),
    h('circle', { cx: '12', cy: '13', r: '4' }),
  ])
}

const PartyIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.6', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M9 18V5l12-2v13' }),
    h('circle', { cx: '6', cy: '18', r: '3' }),
    h('circle', { cx: '18', cy: '16', r: '3' }),
    h('path', { d: 'M4 8l3-3' }),
    h('path', { d: 'M17 4l3 3' }),
  ])
}

const events = [
  {
    time: '7:00 PM',
    tag: 'Arrival',
    title: 'Guest Reception',
    description: 'Welcome drinks and gathering in the grand foyer',
    icon: WelcomeIcon,
  },
  {
    time: '7:45 PM',
    tag: 'Highlights',
    title: 'Grand Zaffa & Entrance',
    description: 'The couple makes their royal entrance',
    icon: ZaffaIcon,
  },
  {
    time: '8:15 PM',
    tag: 'Moments',
    title: 'First Dance & Ring Exchange',
    description: 'Romantic dance and cutting the celebration cake',
    icon: CakeIcon,
  },
  {
    time: '8:45 PM',
    tag: 'Dining',
    title: 'Dinner Banquet',
    description: 'A lavish gourmet dinner buffet for all guests',
    icon: BanquetIcon,
  },
  {
    time: '9:30 PM',
    tag: 'Memories',
    title: 'Photos & Congratulations',
    description: 'Capturing unforgettable moments with family and friends',
    icon: PhotoIcon,
  },
  {
    time: '10:00 PM',
    tag: 'Party',
    title: 'Celebration & Dancing',
    description: 'Live DJ, music, and joyful dancing through the night',
    icon: PartyIcon,
  }
]

const cardRefs = ref([])
const visibleCards = ref(events.map(() => false))
let observers = []

onMounted(() => {
  setTimeout(() => {
    if (!cardRefs.value) return
    const cards = Array.isArray(cardRefs.value) ? cardRefs.value : [cardRefs.value]

    cards.forEach((card, index) => {
      if (!card) return
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              visibleCards.value[index] = true
              observer.unobserve(entry.target)
            }
          })
        },
        { threshold: 0.12 }
      )
      observer.observe(card)
      observers.push(observer)
    })
  }, 100)
})

onUnmounted(() => {
  observers.forEach((obs) => obs.disconnect())
  observers = []
})
</script>

<style scoped>
.agenda {
  padding: 4.5rem 1.25rem;
  background: var(--color-warm-gray);
  position: relative;
  overflow: hidden;
}

.agenda__inner {
  max-width: 440px;
  margin: 0 auto;
}

.agenda__header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.agenda__subheading {
  display: block;
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.4rem;
  font-weight: 500;
}

.agenda__heading {
  font-family: var(--font-serif);
  font-size: 1.85rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-bottom: 0.6rem;
  letter-spacing: 0.02em;
}

.agenda__divider {
  display: block;
  width: 140px;
  height: 18px;
  margin: 0 auto;
  color: var(--color-gold);
}

/* Timeline container with connected track */
.agenda__timeline {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  padding-left: 1.25rem;
}

/* Vertical timeline connector track */
.agenda__track {
  position: absolute;
  top: 1rem;
  bottom: 1.5rem;
  left: 1.7rem;
  width: 2px;
  background: linear-gradient(
    to bottom,
    rgba(196, 164, 155, 0.2) 0%,
    rgba(196, 164, 155, 0.7) 15%,
    rgba(196, 164, 155, 0.7) 85%,
    rgba(196, 164, 155, 0.1) 100%
  );
  z-index: 1;
}

/* Timeline Item */
.agenda__item {
  position: relative;
  display: flex;
  align-items: flex-start;
  gap: 1.25rem;
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1), transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  z-index: 2;
}

.agenda__item--visible {
  opacity: 1;
  transform: translateY(0);
}

/* Timeline Node */
.agenda__node {
  position: relative;
  width: 16px;
  height: 16px;
  margin-top: 1.25rem;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--color-warm-gray);
  border-radius: 50%;
  border: 2px solid var(--color-gold);
  box-shadow: 0 0 0 3px var(--color-warm-gray), 0 2px 8px rgba(74, 20, 26, 0.15);
}

.agenda__node-dot {
  width: 6px;
  height: 6px;
  background: var(--color-navy);
  border-radius: 50%;
}

/* Card */
.agenda__card {
  flex: 1;
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.15rem 1.25rem;
  background: var(--color-ivory);
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(74, 20, 26, 0.05);
  border: 1px solid rgba(196, 164, 155, 0.35);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.agenda__card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(74, 20, 26, 0.09);
  border-color: var(--color-gold);
}

/* Icon */
.agenda__card-icon {
  flex-shrink: 0;
  width: 42px;
  height: 42px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(145deg, #f9f6f0, #efe7dc);
  color: var(--color-navy);
  border-radius: 10px;
  border: 1px solid rgba(196, 164, 155, 0.4);
  box-shadow: 0 2px 8px rgba(74, 20, 26, 0.06);
}

.agenda__card-icon svg {
  width: 22px;
  height: 22px;
}

/* Card Content */
.agenda__card-content {
  flex: 1;
}

.agenda__card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.2rem;
}

.agenda__card-time {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  color: var(--color-navy);
}

.agenda__card-tag {
  font-family: var(--font-sans);
  font-size: 0.55rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  background: rgba(196, 164, 155, 0.15);
  padding: 0.15rem 0.5rem;
  border-radius: 12px;
  font-weight: 600;
}

.agenda__card-title {
  font-family: var(--font-serif);
  font-size: 1.05rem;
  font-weight: 500;
  color: var(--color-navy);
  margin: 0.15rem 0;
  line-height: 1.3;
}

.agenda__card-desc {
  font-family: var(--font-sans);
  font-size: 0.72rem;
  color: var(--color-navy-light);
  line-height: 1.45;
}
</style>
