<template>
  <section class="wishes-section" id="wishes">
    <div class="wishes-section__inner">
      <!-- Section Header (Direct Address to Guests) -->
      <div class="wishes-section__header">
        <span class="wishes-section__eyebrow">دفتر الذكريات والمحبة · Guestbook</span>
        <h2 class="wishes-section__title">شاركونا فرحتنا بكلمة من قلوبكم</h2>

        <svg class="wishes-section__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
          <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
          <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
          <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        </svg>

        <p class="wishes-section__desc">
          يسعدنا أن تتركوا لنا كلمة ودعوة صادقة من قلوبكم تظل تذكاراً جميلاً يرافق بداية رحلتنا معاً 💕
        </p>
      </div>

      <!-- Action Button to write a wish (Direct Address) -->
      <div class="wishes-trigger-wrap">
        <button class="wishes-trigger-btn" @click="openForm">
          <span class="wishes-trigger-btn__shine"></span>
          <span class="wishes-trigger-btn__icon">✍️</span>
          <span>اترك لنا كلمتك ودعواتك الجميلة</span>
          <span class="wishes-trigger-btn__gem">✦</span>
        </button>
      </div>

      <!-- Live Wishes Counter Badge -->
      <div class="wishes-counter">
        <div class="wishes-counter__inner">
          <span class="wishes-counter__pulse"></span>
          <span class="wishes-counter__text">
            {{ wishesList.length > 1 ? `${wishesList.length - 1} رسالة ومحبة شاركتموها معنا` : 'كونوا أول من يشاركنا كلمته الجميلة' }}
          </span>
        </div>
      </div>

      <!-- Wishes Cards List (Royal Parchment Cards) -->
      <div class="wishes-cards">
        <transition-group name="wish-card">
          <div
            v-for="wish in displayedWishes"
            :key="wish.id"
            class="wish-card"
            :class="{ 'wish-card--couple': wish.isCouple }"
          >
            <!-- Inner Hairline Gold Border -->
            <div class="wish-card__inner-frame"></div>

            <!-- Four Corner Gold Ornaments -->
            <span class="wish-card__corner wish-card__corner--tl">✦</span>
            <span class="wish-card__corner wish-card__corner--tr">✦</span>
            <span class="wish-card__corner wish-card__corner--bl">✦</span>
            <span class="wish-card__corner wish-card__corner--br">✦</span>

            <!-- Top Wax Seal Crest -->
            <div class="wish-card__crest-wrap">
              <div class="wish-card__crest" :class="{ 'wish-card__crest--couple': wish.isCouple }">
                <span class="wish-card__crest-icon">{{ wish.stamp || '💍' }}</span>
              </div>
            </div>

            <!-- Author Header -->
            <div class="wish-card__author-wrap">
              <span v-if="wish.isCouple" class="wish-card__couple-tag">
                👑 رسالة من العروسين
              </span>
              <h4 class="wish-card__author" :class="{ 'wish-card__author--couple': wish.isCouple }">
                {{ wish.name }}
              </h4>
              <span class="wish-card__date">{{ wish.date }}</span>
            </div>

            <!-- Ornamental Divider -->
            <div class="wish-card__ornament">
              <span class="wish-card__orn-line"></span>
              <span class="wish-card__orn-diamond">◆</span>
              <span class="wish-card__orn-line"></span>
            </div>

            <!-- Message with Royal Quotes -->
            <div class="wish-card__message-block">
              <span class="quote-mark quote-mark--start">❝</span>
              <p class="wish-card__message">{{ wish.message }}</p>
              <span class="quote-mark quote-mark--end">❞</span>
            </div>

            <!-- Footer -->
            <div class="wish-card__footer">
              <button class="wish-card__like-btn" @click="toggleLike(wish)">
                <span class="wish-card__heart" :class="{ 'wish-card__heart--active': wish.liked }">
                  {{ wish.liked ? '❤️' : '🤍' }}
                </span>
                <span class="wish-card__likes-count">{{ wish.likes || 0 }}</span>
                <span class="wish-card__like-caption">{{ wish.isCouple ? 'محبة وبركة' : 'دعاء ومحبة' }}</span>
              </button>

              <span class="wish-card__signature">Bahaa &amp; Eman</span>
            </div>
          </div>
        </transition-group>
      </div>

      <!-- View more / Collapse toggle -->
      <div v-if="wishesList.length > 4" class="wishes-toggle-wrap">
        <button class="wishes-toggle-btn" @click="showAll = !showAll">
          <span>{{ showAll ? 'عرض أقل' : `عرض باقي الرسائل (${wishesList.length - 4})` }}</span>
          <svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="currentColor" stroke-width="2.2" :class="{ 'icon-rotate': showAll }">
            <polyline points="6 9 12 15 18 9"></polyline>
          </svg>
        </button>
      </div>
    </div>

    <!-- Royal Modal Dialog (Direct Address) -->
    <transition name="modal-pop">
      <div v-if="isFormOpen" class="wishes-modal" @click="closeForm">
        <div class="wishes-modal__backdrop"></div>
        <div class="wishes-modal__dialog" @click.stop>
          <!-- Inner frame -->
          <div class="wishes-modal__frame"></div>

          <!-- Close button -->
          <button class="wishes-modal__close" @click="closeForm" aria-label="Close modal">
            ✕
          </button>

          <!-- Top Crest -->
          <div class="wishes-modal__crest-wrap">
            <div class="wishes-modal__crest">
              <span>💌</span>
            </div>
          </div>

          <h3 class="wishes-modal__title">شاركنا فرحتك ودعواتك الجميلة 💕</h3>
          <p class="wishes-modal__subtitle">اترك لنا كلمة من قلبك تسعدنا وتزيّن دفتر ذكرياتنا</p>

          <form @submit.prevent="submitWish" class="wishes-modal__form">
            <!-- Stamp selector -->
            <div class="wishes-form__group">
              <label class="wishes-form__label">اختر الختم أو الأيقونة المفضلة:</label>
              <div class="wishes-stamps">
                <button
                  type="button"
                  v-for="s in stamps"
                  :key="s"
                  class="wishes-stamp-btn"
                  :class="{ 'wishes-stamp-btn--selected': selectedStamp === s }"
                  @click="selectedStamp = s"
                >
                  {{ s }}
                </button>
              </div>
            </div>

            <!-- Name Input -->
            <div class="wishes-form__group">
              <label for="wish-name" class="wishes-form__label">الاسم الكريم:</label>
              <input
                id="wish-name"
                v-model="formName"
                type="text"
                class="wishes-form__input"
                placeholder="اكتب اسمك الكريم هنا..."
                maxlength="40"
                required
              />
            </div>

            <!-- Message Input -->
            <div class="wishes-form__group">
              <label for="wish-message" class="wishes-form__label">كلمتك ودعواتك لنا:</label>
              <textarea
                id="wish-message"
                v-model="formMessage"
                class="wishes-form__input wishes-form__textarea"
                placeholder="اكتب لنا ما يجول في خاطرك من أمنيات ودعوات صادقة..."
                rows="3"
                maxlength="220"
                required
              ></textarea>
              <span class="wishes-form__char-count">{{ formMessage.length }}/220</span>
            </div>

            <!-- Submit Button -->
            <button type="submit" class="wishes-modal__submit" :disabled="!formName.trim() || !formMessage.trim()">
              <span>مشاركة كلمتك معنا</span>
              <span class="wishes-modal__submit-gem">💍✨</span>
            </button>
          </form>
        </div>
      </div>
    </transition>

    <!-- Celebration Burst on Submission -->
    <div v-if="showHeartsBurst" class="hearts-burst" aria-hidden="true">
      <span v-for="h in 18" :key="h" class="burst-heart" :style="heartBurstStyle(h)">
        {{ ['💖', '💍', '✨', '🌸', '🤍', '🎉'][h % 6] }}
      </span>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// Storage key v3 to clean old dummy data
const STORAGE_KEY = 'bahaa_eman_guestbook_wishes_v3'

const stamps = ['💍', '💖', '🌸', '✨', '🥂', '💌', '🕊️']

// ONLY ONE initial card: Special message from Bahaa & Eman!
const defaultWishes = [
  {
    id: 'couple-message',
    name: 'بهاء & إيمان',
    isCouple: true,
    stamp: '💍',
    message: 'فرحتنا لا تكتمل إلا بوجودكم ومشاركتكم لنا أجمل لحظات العمر.. دعواتكم وكلماتكم الصادقة هي أغلى هدية نستهل بها بداية رحلتنا معاً. ننتظركم بكل حب وشوق لنحتفل معاً في ليلتنا المميزة ❤️✨',
    date: 'من القلب · With All Our Love',
    likes: 18,
    liked: false,
  }
]

const wishesList = ref([])
const isFormOpen = ref(false)
const showAll = ref(false)
const showHeartsBurst = ref(false)

const formName = ref('')
const formMessage = ref('')
const selectedStamp = ref('💍')

const displayedWishes = computed(() => {
  if (showAll.value) return wishesList.value
  return wishesList.value.slice(0, 4)
})

function loadWishes() {
  try {
    const saved = localStorage.getItem(STORAGE_KEY)
    if (saved) {
      const parsed = JSON.parse(saved)
      if (Array.isArray(parsed) && parsed.length > 0) {
        // Ensure couple card is always present at index 0
        const hasCouple = parsed.some(w => w.id === 'couple-message')
        if (!hasCouple) {
          wishesList.value = [defaultWishes[0], ...parsed]
        } else {
          wishesList.value = parsed
        }
      } else {
        wishesList.value = defaultWishes
        saveWishes()
      }
    } else {
      wishesList.value = defaultWishes
      saveWishes()
    }
  } catch (e) {
    wishesList.value = defaultWishes
  }
}

function saveWishes() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(wishesList.value))
  } catch (e) {}
}

function openForm() {
  isFormOpen.value = true
}

function closeForm() {
  isFormOpen.value = false
}

function submitWish() {
  if (!formName.value.trim() || !formMessage.value.trim()) return

  const now = new Date()
  const hours = now.getHours() % 12 || 12
  const minutes = String(now.getMinutes()).padStart(2, '0')
  const period = now.getHours() >= 12 ? 'م' : 'ص'
  const timeStr = `الآن · ${hours}:${minutes} ${period}`

  const newWish = {
    id: Date.now(),
    name: formName.value.trim(),
    stamp: selectedStamp.value,
    message: formMessage.value.trim(),
    date: timeStr,
    likes: 1,
    liked: true,
  }

  // Insert right after the pinned couple's card so the couple's card remains at the very top!
  if (wishesList.value.length > 0 && wishesList.value[0].isCouple) {
    wishesList.value.splice(1, 0, newWish)
  } else {
    wishesList.value.unshift(newWish)
  }
  saveWishes()

  // Reset form
  formName.value = ''
  formMessage.value = ''
  selectedStamp.value = '💍'
  closeForm()

  // Trigger celebration burst
  showHeartsBurst.value = true
  setTimeout(() => {
    showHeartsBurst.value = false
  }, 2200)
}

function toggleLike(wish) {
  wish.liked = !wish.liked
  wish.likes = (wish.likes || 0) + (wish.liked ? 1 : -1)
  saveWishes()
}

function heartBurstStyle(n) {
  const x = Math.random() * 80 + 10
  const y = Math.random() * 80 + 10
  const size = 18 + Math.random() * 16
  const delay = Math.random() * 0.3
  return {
    left: `${x}%`,
    top: `${y}%`,
    fontSize: `${size}px`,
    animationDelay: `${delay}s`,
  }
}

onMounted(() => {
  loadWishes()
})
</script>

<style scoped>
.wishes-section {
  padding: 4.5rem 1.25rem;
  background: var(--color-warm-gray);
  position: relative;
  overflow: hidden;
  direction: rtl;
}

.wishes-section__inner {
  max-width: 420px;
  margin: 0 auto;
}

/* ── Section Header ── */
.wishes-section__header {
  text-align: center;
  margin-bottom: 1.85rem;
}

.wishes-section__eyebrow {
  display: block;
  font-family: var(--font-arabic);
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.4rem;
  font-weight: 600;
}

.wishes-section__title {
  font-family: var(--font-arabic-heading);
  font-size: 1.95rem;
  font-weight: 700;
  color: var(--color-navy);
  margin-bottom: 0.5rem;
  line-height: 1.35;
}

.wishes-section__divider {
  display: block;
  width: 140px;
  height: 18px;
  margin: 0.35rem auto 0.75rem;
  color: var(--color-gold);
}

.wishes-section__desc {
  font-family: var(--font-arabic);
  font-size: 0.82rem;
  font-weight: 400;
  color: var(--color-navy-light);
  line-height: 1.6;
  max-width: 320px;
  margin: 0 auto;
}

/* ── Trigger Button ── */
.wishes-trigger-wrap {
  display: flex;
  justify-content: center;
  margin: 1.75rem 0 1.15rem;
}

.wishes-trigger-btn {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.65rem;
  padding: 0.88rem 1.75rem;
  background: linear-gradient(135deg, #4a141a 0%, #5c1d24 50%, #3a0e13 100%);
  color: #ffffff;
  border: 1.5px solid rgba(212, 175, 55, 0.75);
  border-radius: 30px;
  font-family: var(--font-arabic);
  font-size: 0.88rem;
  font-weight: 600;
  cursor: pointer;
  box-shadow:
    0 10px 30px rgba(74, 20, 26, 0.28),
    0 2px 10px rgba(0, 0, 0, 0.15),
    inset 0 1px 0 rgba(255, 255, 255, 0.25);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  overflow: hidden;
}

.wishes-trigger-btn:hover {
  transform: translateY(-2px) scale(1.02);
  border-color: rgba(212, 175, 55, 1);
  box-shadow: 0 14px 35px rgba(74, 20, 26, 0.4);
}

.wishes-trigger-btn__shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 50%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transform: skewX(-20deg);
  animation: btnShimmer 3.5s infinite;
}

@keyframes btnShimmer {
  0% { left: -100%; }
  40%, 100% { left: 200%; }
}

.wishes-trigger-btn__icon {
  font-size: 1.1rem;
}

.wishes-trigger-btn__gem {
  color: var(--color-gold-light);
  font-size: 0.75rem;
}

/* ── Counter Badge ── */
.wishes-counter {
  display: flex;
  justify-content: center;
  margin-bottom: 1.75rem;
}

.wishes-counter__inner {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.32rem 0.85rem;
  background: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(212, 175, 55, 0.35);
  border-radius: 20px;
  box-shadow: 0 2px 8px rgba(74, 20, 26, 0.05);
  backdrop-filter: blur(4px);
}

.wishes-counter__pulse {
  width: 7px;
  height: 7px;
  background: #2e7d32;
  border-radius: 50%;
  box-shadow: 0 0 0 3px rgba(46, 125, 50, 0.25);
  animation: livePulse 2s infinite ease-in-out;
}

@keyframes livePulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.35); opacity: 0.75; }
}

.wishes-counter__text {
  font-family: var(--font-arabic);
  font-size: 0.72rem;
  font-weight: 500;
  color: var(--color-navy);
}

/* ── Royal Parchment Cards ── */
.wishes-cards {
  display: flex;
  flex-direction: column;
  gap: 1.35rem;
}

.wish-card {
  position: relative;
  background: linear-gradient(168deg, #ffffff 0%, #faf6f0 55%, #f4eee5 100%);
  border-radius: 18px;
  padding: 1.75rem 1.45rem 1.35rem;
  box-shadow:
    0 12px 35px rgba(74, 20, 26, 0.08),
    0 2px 8px rgba(0, 0, 0, 0.04),
    inset 0 0 0 1px rgba(255, 255, 255, 0.95);
  border: 1.5px solid rgba(212, 175, 55, 0.45);
  transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
  overflow: hidden;
}

.wish-card:hover {
  transform: translateY(-3px);
  border-color: rgba(212, 175, 55, 0.85);
  box-shadow:
    0 16px 42px rgba(74, 20, 26, 0.14),
    0 4px 12px rgba(212, 175, 55, 0.2);
}

/* Distinctive glow for Couple card */
.wish-card--couple {
  border-color: rgba(212, 175, 55, 0.75);
  background: linear-gradient(168deg, #ffffff 0%, #fffcf8 45%, #f9f2e7 100%);
  box-shadow:
    0 14px 38px rgba(74, 20, 26, 0.12),
    0 3px 12px rgba(212, 175, 55, 0.25),
    inset 0 0 0 1px rgba(255, 255, 255, 1);
}

/* Inner hairline gold frame */
.wish-card__inner-frame {
  position: absolute;
  inset: 7px;
  border: 1px solid rgba(212, 175, 55, 0.25);
  border-radius: 13px;
  pointer-events: none;
}

/* Four Corner Flourishes */
.wish-card__corner {
  position: absolute;
  font-size: 0.5rem;
  color: rgba(212, 175, 55, 0.7);
  line-height: 1;
  pointer-events: none;
}

.wish-card__corner--tl { top: 12px; right: 12px; }
.wish-card__corner--tr { top: 12px; left: 12px; }
.wish-card__corner--bl { bottom: 12px; right: 12px; }
.wish-card__corner--br { bottom: 12px; left: 12px; }

/* Top Crest */
.wish-card__crest-wrap {
  display: flex;
  justify-content: center;
  margin-top: -0.25rem;
  margin-bottom: 0.65rem;
}

.wish-card__crest {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  background: radial-gradient(circle at 35% 35%, #5c1d24 0%, #4a141a 70%, #2f0a10 100%);
  border: 1.5px solid rgba(212, 175, 55, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(74, 20, 26, 0.25);
}

.wish-card__crest--couple {
  border-color: #d4af37;
  box-shadow: 0 4px 16px rgba(212, 175, 55, 0.4);
}

.wish-card__crest-icon {
  font-size: 1.15rem;
  line-height: 1;
}

/* Author Info */
.wish-card__author-wrap {
  text-align: center;
}

.wish-card__couple-tag {
  display: inline-block;
  font-family: var(--font-arabic);
  font-size: 0.62rem;
  font-weight: 700;
  color: #7b2128;
  background: rgba(212, 175, 55, 0.18);
  border: 1px solid rgba(212, 175, 55, 0.5);
  border-radius: 12px;
  padding: 0.15rem 0.65rem;
  margin-bottom: 0.35rem;
}

.wish-card__author {
  font-family: var(--font-arabic);
  font-size: 1.02rem;
  font-weight: 700;
  color: var(--color-navy);
  letter-spacing: 0.01em;
  margin-bottom: 0.15rem;
}

.wish-card__author--couple {
  font-family: var(--font-arabic-heading);
  font-size: 1.25rem;
  color: #4a141a;
}

.wish-card__date {
  font-family: var(--font-arabic);
  font-size: 0.65rem;
  font-weight: 400;
  color: var(--color-navy-light);
  opacity: 0.75;
}

/* Ornamental Divider */
.wish-card__ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.45rem;
  margin: 0.7rem 0 0.85rem;
}

.wish-card__orn-line {
  width: 32px;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(212, 175, 55, 0.5), transparent);
}

.wish-card__orn-diamond {
  font-size: 0.35rem;
  color: var(--color-gold);
}

/* Message Block */
.wish-card__message-block {
  position: relative;
  padding: 0 0.5rem;
  text-align: center;
  margin-bottom: 1rem;
}

.quote-mark {
  font-family: var(--font-serif);
  font-size: 1.15rem;
  color: var(--color-gold);
  line-height: 1;
  opacity: 0.8;
  display: inline-block;
  vertical-align: middle;
}

.quote-mark--start {
  margin-left: 0.25rem;
}

.quote-mark--end {
  margin-right: 0.25rem;
}

.wish-card__message {
  display: inline;
  font-family: var(--font-arabic-heading);
  font-size: 1.05rem;
  font-weight: 400;
  line-height: 1.85;
  color: #3b1016;
  text-align: center;
}

/* Footer */
.wish-card__footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 0.75rem;
  border-top: 1px dashed rgba(212, 175, 55, 0.35);
  margin-top: 0.25rem;
}

.wish-card__like-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(212, 175, 55, 0.4);
  border-radius: 20px;
  padding: 0.25rem 0.65rem;
  cursor: pointer;
  font-family: var(--font-arabic);
  font-size: 0.7rem;
  color: var(--color-navy);
  box-shadow: 0 2px 6px rgba(74, 20, 26, 0.04);
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.wish-card__like-btn:hover {
  transform: scale(1.08);
  border-color: rgba(212, 175, 55, 0.8);
}

.wish-card__heart--active {
  animation: heartPop 0.35s ease;
}

.wish-card__like-caption {
  font-size: 0.62rem;
  color: var(--color-navy-light);
  opacity: 0.8;
}

.wish-card__signature {
  font-family: var(--font-cursive);
  font-size: 1.25rem;
  color: #5c1d24;
  letter-spacing: 0.02em;
}

/* ── Toggle Button ── */
.wishes-toggle-wrap {
  text-align: center;
  margin-top: 1.4rem;
}

.wishes-toggle-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  background: rgba(255, 255, 255, 0.6);
  border: 1px solid rgba(212, 175, 55, 0.35);
  font-family: var(--font-arabic);
  font-size: 0.78rem;
  font-weight: 600;
  color: var(--color-navy);
  cursor: pointer;
  padding: 0.45rem 1.1rem;
  border-radius: 20px;
  transition: all 0.2s ease;
}

.wishes-toggle-btn:hover {
  background: #ffffff;
  border-color: rgba(212, 175, 55, 0.7);
  box-shadow: 0 4px 12px rgba(74, 20, 26, 0.08);
}

.icon-rotate {
  transform: rotate(180deg);
}

/* ── Modal Dialog ── */
.wishes-modal {
  position: fixed;
  inset: 0;
  z-index: 10000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.25rem;
  direction: rtl;
}

.wishes-modal__backdrop {
  position: absolute;
  inset: 0;
  background: rgba(25, 4, 8, 0.82);
  backdrop-filter: blur(10px);
}

.wishes-modal__dialog {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 390px;
  background: linear-gradient(168deg, #ffffff 0%, #faf6f0 60%, #f4ece2 100%);
  border-radius: 22px;
  padding: 2.1rem 1.5rem 1.65rem;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.45);
  border: 1.5px solid rgba(212, 175, 55, 0.6);
  text-align: center;
  overflow: hidden;
}

.wishes-modal__frame {
  position: absolute;
  inset: 7px;
  border: 1px solid rgba(212, 175, 55, 0.25);
  border-radius: 16px;
  pointer-events: none;
}

.wishes-modal__close {
  position: absolute;
  top: 14px;
  left: 14px;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: rgba(74, 20, 26, 0.06);
  border: 1px solid rgba(212, 175, 55, 0.25);
  font-size: 0.9rem;
  color: var(--color-navy);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  z-index: 5;
}

.wishes-modal__close:hover {
  background: rgba(74, 20, 26, 0.15);
  transform: rotate(90deg);
}

.wishes-modal__crest-wrap {
  display: flex;
  justify-content: center;
  margin-bottom: 0.65rem;
}

.wishes-modal__crest {
  width: 52px;
  height: 52px;
  border-radius: 50%;
  background: radial-gradient(circle at 35% 35%, #5c1d24 0%, #4a141a 70%, #2f0a10 100%);
  border: 1.5px solid rgba(212, 175, 55, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  box-shadow: 0 4px 16px rgba(74, 20, 26, 0.3);
}

.wishes-modal__title {
  font-family: var(--font-arabic-heading);
  font-size: 1.55rem;
  font-weight: 700;
  color: var(--color-navy);
  margin-bottom: 0.25rem;
}

.wishes-modal__subtitle {
  font-family: var(--font-arabic);
  font-size: 0.75rem;
  color: var(--color-navy-light);
  margin-bottom: 1.35rem;
  line-height: 1.45;
}

.wishes-modal__form {
  display: flex;
  flex-direction: column;
  gap: 1.05rem;
  text-align: right;
}

.wishes-form__group {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
  position: relative;
}

.wishes-form__label {
  font-family: var(--font-arabic);
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--color-navy);
}

/* Stamps Row */
.wishes-stamps {
  display: flex;
  gap: 0.4rem;
  justify-content: center;
  padding: 0.25rem 0;
}

.wishes-stamp-btn {
  font-size: 1.3rem;
  width: 40px;
  height: 40px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.9);
  border: 1.5px solid rgba(212, 175, 55, 0.25);
  cursor: pointer;
  transition: transform 0.2s ease, border-color 0.2s ease;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.04);
}

.wishes-stamp-btn:hover {
  transform: scale(1.15);
  border-color: rgba(212, 175, 55, 0.7);
}

.wishes-stamp-btn--selected {
  border-color: #d4af37;
  background: rgba(212, 175, 55, 0.18);
  transform: scale(1.15);
  box-shadow: 0 4px 10px rgba(212, 175, 55, 0.3);
}

.wishes-form__input {
  width: 100%;
  padding: 0.8rem 1rem;
  background: #ffffff;
  border: 1.5px solid rgba(212, 175, 55, 0.3);
  border-radius: 12px;
  font-family: var(--font-arabic);
  font-size: 0.88rem;
  color: var(--color-navy);
  outline: none;
  transition: all 0.25s ease;
  box-sizing: border-box;
}

.wishes-form__input:focus {
  border-color: #d4af37;
  box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.25);
}

.wishes-form__textarea {
  resize: none;
  line-height: 1.6;
}

.wishes-form__char-count {
  font-family: var(--font-arabic);
  font-size: 0.62rem;
  color: var(--color-navy-light);
  opacity: 0.65;
  text-align: left;
  margin-top: 2px;
}

.wishes-modal__submit {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  width: 100%;
  padding: 0.9rem;
  margin-top: 0.5rem;
  background: linear-gradient(135deg, #4a141a 0%, #5c1d24 60%, #3a0e13 100%);
  color: #ffffff;
  border: 1.5px solid rgba(212, 175, 55, 0.7);
  border-radius: 14px;
  font-family: var(--font-arabic);
  font-size: 0.9rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.25s ease;
  box-shadow: 0 6px 18px rgba(74, 20, 26, 0.3);
}

.wishes-modal__submit:hover:not(:disabled) {
  background: linear-gradient(135deg, #5c1820 0%, #70212a 100%);
  border-color: rgba(212, 175, 55, 1);
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(74, 20, 26, 0.4);
}

.wishes-modal__submit:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

/* ── Celebration Hearts ── */
.hearts-burst {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 10005;
}

.burst-heart {
  position: absolute;
  animation: floatUpBurst 1.8s ease-out forwards;
}

@keyframes floatUpBurst {
  0%   { opacity: 1; transform: translateY(0) scale(0.5); }
  50%  { opacity: 1; transform: translateY(-40px) scale(1.3); }
  100% { opacity: 0; transform: translateY(-90px) scale(0.8); }
}

@keyframes heartPop {
  0%   { transform: scale(0.8); }
  50%  { transform: scale(1.4); }
  100% { transform: scale(1); }
}

/* Transitions */
.wish-card-enter-active {
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.wish-card-enter-from {
  opacity: 0;
  transform: translateY(20px) scale(0.95);
}

.modal-pop-enter-active,
.modal-pop-leave-active {
  transition: opacity 0.3s ease, transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-pop-enter-from,
.modal-pop-leave-to {
  opacity: 0;
  transform: scale(0.92);
}
</style>
