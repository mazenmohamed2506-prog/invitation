<template>
  <section class="rsvp" id="rsvp">
    <div class="rsvp__inner">
      <h2 class="rsvp__heading">RSVP</h2>
      <p class="rsvp__subheading">We would love to hear from you</p>

      <svg class="rsvp__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
        <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
        <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
      </svg>

      <form class="rsvp__form" @submit.prevent="handleSubmit">
        <div class="rsvp__field">
          <label for="rsvp-name" class="rsvp__label">Your Name</label>
          <input
            id="rsvp-name"
            v-model="name"
            type="text"
            class="rsvp__input"
            placeholder="Enter your full name"
            required
          />
        </div>

        <div class="rsvp__field">
          <label for="rsvp-guests" class="rsvp__label">Number of Guests</label>
          <select
            id="rsvp-guests"
            v-model="guests"
            class="rsvp__input rsvp__select"
            required
          >
            <option value="" disabled>Select number of guests</option>
            <option v-for="n in 10" :key="n" :value="n">{{ n }} {{ n === 1 ? 'Guest' : 'Guests' }}</option>
          </select>
        </div>

        <button type="submit" class="rsvp__submit" :disabled="!isValid">
          <svg class="rsvp__whatsapp-icon" viewBox="0 0 24 24" fill="currentColor">
            <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
          </svg>
          Confirm via WhatsApp
        </button>
      </form>

      <p class="rsvp__footer">
        Kindly confirm by <strong>October 15, 2026</strong>
      </p>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const WHATSAPP_NUMBER = '201099528007'

const name = ref('')
const guests = ref('')

const isValid = computed(() => name.value.trim() && guests.value)

function handleSubmit() {
  if (!isValid.value) return

  const message = `Hello, I am ${name.value.trim()}. I am confirming my attendance at the engagement of Bahaa & Eman with ${guests.value} guest${guests.value > 1 ? 's' : ''}.`
  const encodedMessage = encodeURIComponent(message)
  const url = `https://wa.me/${WHATSAPP_NUMBER}?text=${encodedMessage}`

  window.open(url, '_blank')
}
</script>

<style scoped>
.rsvp {
  padding: 4rem 1.5rem;
  background: var(--color-warm-gray-dark);
}

.rsvp__inner {
  max-width: 400px;
  margin: 0 auto;
  text-align: center;
}

.rsvp__heading {
  font-family: var(--font-serif);
  font-size: 1.75rem;
  font-weight: 500;
  color: var(--color-navy);
  letter-spacing: 0.1em;
}

.rsvp__subheading {
  font-family: var(--font-sans);
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  color: var(--color-navy-light);
  margin-top: 0.5rem;
}

.rsvp__divider {
  display: block;
  width: 140px;
  height: 20px;
  margin: 1rem auto 2rem;
  color: var(--color-gold);
}

.rsvp__form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  text-align: left;
}

.rsvp__field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.rsvp__label {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-navy);
}

.rsvp__input {
  width: 100%;
  padding: 0.85rem 1rem;
  background: var(--color-ivory);
  border: 1.5px solid rgba(75, 61, 91, 0.15);
  border-radius: 8px;
  color: var(--color-navy);
  font-family: var(--font-sans);
  font-size: 0.9rem;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  outline: none;
}

.rsvp__input::placeholder {
  color: rgba(75, 61, 91, 0.4);
}

.rsvp__input:focus {
  border-color: var(--color-gold);
  box-shadow: 0 0 0 3px rgba(201, 169, 110, 0.15);
}

.rsvp__select {
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%23c9a96e' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 1rem center;
  cursor: pointer;
}

.rsvp__select option {
  background: var(--color-ivory);
  color: var(--color-navy);
}

.rsvp__submit {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  width: 100%;
  padding: 1rem;
  margin-top: 0.75rem;
  background: linear-gradient(135deg, var(--color-gold-dark), var(--color-gold), var(--color-gold-light));
  color: var(--color-navy-dark);
  border: none;
  border-radius: 8px;
  font-family: var(--font-sans);
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(201, 169, 110, 0.25);
}

.rsvp__submit:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 6px 25px rgba(201, 169, 110, 0.4);
}

.rsvp__submit:active:not(:disabled) {
  transform: translateY(0);
}

.rsvp__submit:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

.rsvp__whatsapp-icon {
  width: 20px;
  height: 20px;
}

.rsvp__footer {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  color: var(--color-gold-light);
  opacity: 0.6;
  margin-top: 2rem;
}

.rsvp__footer strong {
  color: var(--color-gold);
  font-weight: 500;
}
</style>
