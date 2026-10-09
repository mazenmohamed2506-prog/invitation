<template>
  <section class="venue-rules" id="venue">
    <div class="venue-rules__inner">
      <!-- Venue Section -->
      <h2 class="venue-rules__heading">The Venue</h2>

      <svg class="venue-rules__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
        <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
        <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
      </svg>

      <!-- 3D Flip Card: Front is Map, Back is QR -->
      <div class="flip-card" @click="isFlipped = !isFlipped">
        <div class="flip-card__inner" :class="{ 'flip-card__inner--flipped': isFlipped }">
          <!-- Front Face: Venue & Interactive Map -->
          <div class="flip-card__face flip-card__front">
            <div class="flip-card__front-inner">
              <span class="flip-card__tag">Engagement Party</span>
              <h3 class="flip-card__venue-title">Cicada Hall</h3>
              <p class="flip-card__venue-location">Armed Forces Club · Zamalek, Cairo</p>

              <!-- Clickable Map Preview (OSM footer and zoom controls completely clipped) -->
              <a 
                :href="mapLocationUrl" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="flip-card__map-card"
                title="Open in Google Maps"
                @click.stop
              >
                <div class="flip-card__map-frame">
                  <iframe 
                    class="flip-card__map-iframe"
                    :src="mapEmbedUrl"
                    loading="lazy"
                    scrolling="no"
                    frameborder="0"
                    tabindex="-1"
                    aria-hidden="true"
                  ></iframe>

                  <!-- Animated Luxury Gold Pin -->
                  <div class="flip-card__map-overlay">
                    <div class="flip-card__pin-container">
                      <div class="flip-card__pin-pulse"></div>
                      <div class="flip-card__pin-marker">
                        <svg viewBox="0 0 24 24" class="flip-card__pin-svg" fill="currentColor">
                          <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/>
                        </svg>
                      </div>
                      <span class="flip-card__pin-badge">Cicada Hall</span>
                    </div>

                    <div class="flip-card__map-badge">
                      <svg viewBox="0 0 24 24" width="11" height="11" fill="none" stroke="currentColor" stroke-width="2.5">
                        <polygon points="3 11 22 2 13 21 11 13 3 11"></polygon>
                      </svg>
                      <span>Tap for GPS</span>
                    </div>
                  </div>
                </div>
              </a>

              <!-- Direct Google Maps CTA -->
              <a 
                :href="mapLocationUrl" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="flip-card__maps-button"
                @click.stop
              >
                <svg viewBox="0 0 24 24" width="15" height="15" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
                  <circle cx="12" cy="10" r="3"></circle>
                </svg>
                <span>Open in Google Maps</span>
                <svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                  <line x1="7" y1="17" x2="17" y2="7"></line>
                  <polyline points="7 7 17 7 17 17"></polyline>
                </svg>
              </a>

              <p class="flip-card__address-tag">
                26th of July St, Zamalek · Cairo
              </p>
            </div>

            <!-- Hint: Tap to flip to QR Code -->
            <div class="flip-card__hint-wrap">
              <span class="flip-card__hint-text">
                <svg viewBox="0 0 24 24" width="12" height="12" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="3" width="7" height="7"></rect>
                  <rect x="14" y="3" width="7" height="7"></rect>
                  <rect x="14" y="14" width="7" height="7"></rect>
                  <rect x="3" y="14" width="7" height="7"></rect>
                </svg>
                Tap card to view QR Code
              </span>
            </div>
          </div>

          <!-- Back Face: QR Code -->
          <div class="flip-card__face flip-card__back">
            <div class="flip-card__qr-content">
              <span class="flip-card__back-badge">Scan for Directions</span>
              <h3 class="flip-card__qr-title">Cicada Hall</h3>
              <p class="flip-card__qr-hall">Armed Forces Club · Zamalek</p>

              <div class="flip-card__qr-frame">
                <img :src="qrCodeDataUrl" alt="Venue QR code" class="flip-card__qr-image" />
              </div>

              <p class="flip-card__qr-subtitle">Scan with camera for instant directions</p>

              <a 
                :href="mapLocationUrl" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="flip-card__maps-button flip-card__maps-button--compact"
                @click.stop
              >
                <svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
                  <polyline points="15 3 21 3 21 9"></polyline>
                  <line x1="10" y1="14" x2="21" y2="3"></line>
                </svg>
                <span>Open in Google Maps</span>
              </a>
            </div>

            <div class="flip-card__back-hint">
              <svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M3 12a9 9 0 1 0 9-9 9.75 9.75 0 0 0-6.74 2.74L3 8"/>
                <path d="M3 3v5h5"/>
              </svg>
              <span>Tap to flip back to map</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import qrCodeImg from '@/assets/images/qr-code.png'
import QRCode from 'qrcode'

const isFlipped = ref(false)
const mapLocationUrl = 'https://maps.app.goo.gl/Jv6Bmiv6MFimiugMA?g_st=iw'
const qrCodeDataUrl = ref(qrCodeImg)

// Center coordinates for Cicada Hall - Armed Forces Club (Zamalek, Cairo)
// Notice: No &marker=... parameter so the green Leaflet marker is not drawn
const mapEmbedUrl = 'https://www.openstreetmap.org/export/embed.html?bbox=31.212%2C30.050%2C31.228%2C30.062&layer=mapnik'

onMounted(async () => {
  try {
    qrCodeDataUrl.value = await QRCode.toDataURL(mapLocationUrl, {
      color: { dark: '#4a141aff', light: '#fbf8f5ff' },
      width: 400,
      margin: 2
    })
  } catch (e) {
    qrCodeDataUrl.value = qrCodeImg
  }
})
</script>

<style scoped>
.venue-rules {
  padding: 4rem 1.5rem;
  background: var(--color-warm-gray);
}

.venue-rules__inner {
  max-width: 400px;
  margin: 0 auto;
}

.venue-rules__heading {
  font-family: var(--font-serif);
  font-size: 1.75rem;
  font-weight: 500;
  color: var(--color-navy);
  text-align: center;
  margin-bottom: 0.75rem;
}

.venue-rules__heading--rules {
  margin-top: 3rem;
}

.venue-rules__divider {
  display: block;
  width: 140px;
  height: 20px;
  margin: 0 auto 2rem;
  color: var(--color-gold);
}

/* ── Flip Card ── */
.flip-card {
  perspective: 1000px;
  cursor: pointer;
  margin: 0 auto;
  max-width: 320px;
}

.flip-card__inner {
  position: relative;
  width: 100%;
  aspect-ratio: 3 / 4.35;
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  transform-style: preserve-3d;
}

.flip-card__inner--flipped {
  transform: rotateY(180deg);
}

.flip-card__face {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 16px 42px rgba(74, 20, 26, 0.16), 0 3px 10px rgba(0, 0, 0, 0.08);
  border: 1.5px solid rgba(212, 175, 55, 0.45);
}

/* Front Face: Venue & Map */
.flip-card__front {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background: linear-gradient(168deg, #ffffff 0%, #fbf8f4 60%, #f4efe8 100%);
  padding: 1.25rem 1rem 0.95rem;
}

.flip-card__front-inner {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  width: 100%;
}

.flip-card__tag {
  font-family: var(--font-cinzel, var(--font-serif));
  font-size: 0.6rem;
  font-weight: 700;
  letter-spacing: 0.24em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.25rem;
}

.flip-card__venue-title {
  font-family: var(--font-serif);
  font-size: 1.35rem;
  font-weight: 600;
  color: #4a141a;
  letter-spacing: 0.02em;
  margin: 0;
  line-height: 1.25;
}

.flip-card__venue-location {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  margin-top: 0.15rem;
  margin-bottom: 0.65rem;
  opacity: 0.85;
}

/* Map Card */
.flip-card__map-card {
  position: relative;
  width: 100%;
  height: 185px;
  border-radius: 14px;
  overflow: hidden;
  border: 1.5px solid rgba(212, 175, 55, 0.45);
  box-shadow: 0 4px 16px rgba(74, 20, 26, 0.12);
  display: block;
  text-decoration: none;
  background: #e5e3df;
  cursor: pointer;
  transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease;
}

.flip-card__map-card:hover {
  transform: translateY(-2px);
  border-color: rgba(212, 175, 55, 0.85);
  box-shadow: 0 6px 22px rgba(74, 20, 26, 0.22);
}

.flip-card__map-frame {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  border-radius: 12px;
}

/* Precise CSS clipping: top -46px clips zoom controls; height +84px extends past container clipping the OSM attribution/donation footer! */
.flip-card__map-iframe {
  position: absolute;
  top: -46px;
  left: -5px;
  width: calc(100% + 10px);
  height: calc(100% + 84px);
  border: none;
  pointer-events: none;
  filter: saturate(1.15) contrast(1.05);
}

.flip-card__map-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: radial-gradient(circle at center, rgba(255, 255, 255, 0.05) 0%, rgba(20, 25, 35, 0.24) 100%);
  pointer-events: none;
}

/* Custom Animated Pin */
.flip-card__pin-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  transform: translateY(-4px);
}

.flip-card__pin-pulse {
  position: absolute;
  top: 6px;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: rgba(212, 175, 55, 0.35);
  animation: mapPinPulse 2.2s infinite ease-out;
  pointer-events: none;
}

.flip-card__pin-marker {
  width: 30px;
  height: 30px;
  color: #4a141a;
  filter: drop-shadow(0 2px 6px rgba(0, 0, 0, 0.35));
  z-index: 2;
  animation: mapPinBounce 2.5s infinite ease-in-out;
}

.flip-card__pin-svg {
  width: 100%;
  height: 100%;
}

.flip-card__pin-badge {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: #4a141a;
  background: rgba(255, 255, 255, 0.94);
  padding: 0.18rem 0.55rem;
  border-radius: 10px;
  border: 1px solid rgba(212, 175, 55, 0.6);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  margin-top: 0.15rem;
  white-space: nowrap;
  z-index: 2;
}

.flip-card__map-badge {
  position: absolute;
  bottom: 8px;
  right: 8px;
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  font-family: var(--font-sans);
  font-size: 0.55rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #ffffff;
  background: rgba(74, 20, 26, 0.88);
  backdrop-filter: blur(4px);
  padding: 0.25rem 0.6rem;
  border-radius: 12px;
  border: 1px solid rgba(212, 175, 55, 0.5);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
}

@keyframes mapPinPulse {
  0% { transform: scale(0.6); opacity: 0.9; }
  100% { transform: scale(1.8); opacity: 0; }
}

@keyframes mapPinBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-4px); }
}

/* Maps CTA Button */
.flip-card__maps-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  width: 100%;
  margin-top: 0.65rem;
  padding: 0.58rem 1rem;
  background: linear-gradient(135deg, #4a141a 0%, #6b1d26 100%);
  color: #ffffff;
  border: 1.5px solid rgba(212, 175, 55, 0.6);
  border-radius: 25px;
  font-family: var(--font-sans);
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  text-decoration: none;
  box-shadow: 0 4px 14px rgba(74, 20, 26, 0.22);
  transition: all 0.3s ease;
  box-sizing: border-box;
}

.flip-card__maps-button:hover {
  background: linear-gradient(135deg, #5c1821 0%, #7d222d 100%);
  border-color: rgba(212, 175, 55, 0.9);
  transform: translateY(-1px);
  box-shadow: 0 6px 18px rgba(74, 20, 26, 0.32);
}

.flip-card__maps-button--compact {
  max-width: 220px;
  margin-top: 0.75rem;
}

.flip-card__address-tag {
  font-family: var(--font-sans);
  font-size: 0.62rem;
  letter-spacing: 0.08em;
  color: var(--color-navy-light);
  margin-top: 0.35rem;
  margin-bottom: 0.15rem;
  opacity: 0.85;
}

.flip-card__hint-wrap {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: 0.25rem;
}

.flip-card__hint-text {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  font-family: var(--font-sans);
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  padding: 0.35rem 0.75rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.04);
  opacity: 0.85;
  transition: all 0.2s ease;
}

.flip-card:hover .flip-card__hint-text {
  background: rgba(212, 175, 55, 0.15);
  color: #4a141a;
  opacity: 1;
}

/* Back Face: QR Code */
.flip-card__back {
  transform: rotateY(180deg);
  background: linear-gradient(160deg, var(--color-warm-gray-dark), var(--color-ivory));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 1.25rem 1rem 0.95rem;
}

.flip-card__qr-content {
  text-align: center;
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.flip-card__back-badge {
  font-family: var(--font-sans);
  font-size: 0.55rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.15rem;
}

.flip-card__qr-title {
  font-family: var(--font-serif);
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--color-navy);
  margin: 0;
  line-height: 1.25;
}

.flip-card__qr-hall {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-top: 0.15rem;
  margin-bottom: 0.75rem;
}

.flip-card__qr-frame {
  width: 155px;
  height: 155px;
  padding: 10px;
  background: var(--color-ivory);
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(74, 20, 26, 0.15);
  border: 1px solid rgba(196, 164, 155, 0.4);
}

.flip-card__qr-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.flip-card__qr-subtitle {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  color: var(--color-navy-light);
  margin-top: 0.75rem;
  opacity: 0.8;
}

.flip-card__back-hint {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  padding: 0.4rem 0.8rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.04);
  opacity: 0.85;
}

/* ── Rules ── */
.rules {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1.5rem;
}

.rules__card {
  background: var(--color-ivory);
  border-radius: 8px;
  padding: 1.5rem;
  text-align: center;
  box-shadow: 0 2px 12px rgba(74, 20, 26, 0.05);
  border: 1px solid var(--color-warm-gray-dark);
}

.rules__icon {
  width: 44px;
  height: 44px;
  margin: 0 auto 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-gold);
}

.rules__icon svg {
  width: 28px;
  height: 28px;
}

.rules__title {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-bottom: 0.5rem;
}

.rules__desc {
  font-family: var(--font-sans);
  font-size: 0.78rem;
  color: var(--color-navy-light);
  line-height: 1.6;
}

.rules__subdesc {
  font-size: 0.7rem;
  opacity: 0.6;
}
</style>
