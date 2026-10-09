<template>
  <section class="gallery-section" id="gallery">
    <!-- Gentle floating background petals -->
    <div class="gallery-petals" aria-hidden="true">
      <span v-for="p in 6" :key="'petal-'+p" class="gallery-petal" :style="petalStyle(p)">
        <svg viewBox="0 0 24 24" width="18" height="18" fill="none">
          <path d="M12 2 C 16 6, 20 11, 16 17 C 12 21, 6 19, 4 14 C 2 9, 7 4, 12 2 Z"
            fill="rgba(224, 185, 188, 0.45)"
            stroke="rgba(196, 148, 155, 0.35)"
            stroke-width="0.7"/>
          <path d="M12 5 C 13 9, 12 14, 9 17" stroke="rgba(240, 215, 218, 0.6)" stroke-width="0.5" fill="none"/>
        </svg>
      </span>
    </div>

    <div class="gallery-section__inner">
      <!-- Section Header -->
      <div class="gallery-section__header">
        <span class="gallery-section__eyebrow">Captured Moments · لحظات لا تُنسى</span>
        <h2 class="gallery-section__title">Our Moments of Love</h2>

        <svg class="gallery-section__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
          <!-- Delicate Rosebud Centerpiece in Divider -->
          <g transform="translate(100, 10)">
            <circle cx="0" cy="0" r="3.5" fill="var(--color-gold)" opacity="0.9"/>
            <path d="M-2 -1 C-2 -3, 2 -3, 2 -1 C2 1, -1 2, 0 0" stroke="#5c1d24" stroke-width="0.6" fill="none"/>
          </g>
          <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
          <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        </svg>
      </div>

      <!-- Wrapper for Showcase Card with Corner Florals -->
      <div class="gallery-card-wrapper">
        <!-- Top Left Corner Floral -->
        <svg class="gallery-floral gallery-floral--tl" viewBox="0 0 90 90" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <defs>
            <linearGradient id="goldFloraGradTL" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#d4af37" stop-opacity="0.95"/>
              <stop offset="60%" stop-color="#c59b6d" stop-opacity="0.85"/>
              <stop offset="100%" stop-color="#e8c4c8" stop-opacity="0.9"/>
            </linearGradient>
            <radialGradient id="petalGlowTL" cx="50%" cy="50%" r="50%">
              <stop offset="0%" stop-color="#fdf2f4" stop-opacity="0.95"/>
              <stop offset="100%" stop-color="#d99b9e" stop-opacity="0.6"/>
            </radialGradient>
          </defs>
          <!-- Branch -->
          <path d="M6 84 C 18 52, 42 24, 84 8" stroke="url(#goldFloraGradTL)" stroke-width="1.3" stroke-linecap="round"/>
          <path d="M32 54 C 20 42, 16 28, 22 16 C 26 24, 30 36, 36 44" stroke="url(#goldFloraGradTL)" stroke-width="0.9" fill="rgba(216, 200, 184, 0.2)"/>
          <path d="M50 36 C 42 22, 48 12, 58 14 C 58 22, 54 30, 50 36Z" fill="rgba(216, 200, 184, 0.25)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M22 66 C 10 68, 6 60, 10 52 C 16 56, 20 62, 22 66Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M68 20 C 72 8, 82 8, 84 14 C 80 20, 74 20, 68 20Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <!-- Central Rose -->
          <g transform="translate(36, 38)">
            <path d="M-9 -3 C-10 -11, 4 -12, 8 -4 C12 4, -4 12, -9 -3Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-4 -8 C4 -12, 12 -4, 8 4 C3 10, -8 6, -4 -8Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-3 -2 C-3 -6, 3 -6, 3 -2 C3 2, -1 3, -1 1 C-1 0, 1 0, 1 -1" stroke="#8b4a52" stroke-width="0.9" fill="none" stroke-linecap="round"/>
            <circle cx="0" cy="0" r="2.2" fill="#e8b8be"/>
          </g>
          <!-- Buds -->
          <g transform="translate(74, 12)">
            <path d="M0 6 C-4 2, -2 -3, 2 -4 C6 -2, 5 3, 0 6Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
          <g transform="translate(18, 20)">
            <path d="M0 5 C-3 2, -2 -2, 1 -3 C4 -1, 3 3, 0 5Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
        </svg>

        <!-- Top Right Corner Floral -->
        <svg class="gallery-floral gallery-floral--tr" viewBox="0 0 90 90" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <path d="M6 84 C 18 52, 42 24, 84 8" stroke="url(#goldFloraGradTL)" stroke-width="1.3" stroke-linecap="round"/>
          <path d="M32 54 C 20 42, 16 28, 22 16 C 26 24, 30 36, 36 44" stroke="url(#goldFloraGradTL)" stroke-width="0.9" fill="rgba(216, 200, 184, 0.2)"/>
          <path d="M50 36 C 42 22, 48 12, 58 14 C 58 22, 54 30, 50 36Z" fill="rgba(216, 200, 184, 0.25)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M22 66 C 10 68, 6 60, 10 52 C 16 56, 20 62, 22 66Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M68 20 C 72 8, 82 8, 84 14 C 80 20, 74 20, 68 20Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <g transform="translate(36, 38)">
            <path d="M-9 -3 C-10 -11, 4 -12, 8 -4 C12 4, -4 12, -9 -3Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-4 -8 C4 -12, 12 -4, 8 4 C3 10, -8 6, -4 -8Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-3 -2 C-3 -6, 3 -6, 3 -2 C3 2, -1 3, -1 1 C-1 0, 1 0, 1 -1" stroke="#8b4a52" stroke-width="0.9" fill="none" stroke-linecap="round"/>
            <circle cx="0" cy="0" r="2.2" fill="#e8b8be"/>
          </g>
          <g transform="translate(74, 12)">
            <path d="M0 6 C-4 2, -2 -3, 2 -4 C6 -2, 5 3, 0 6Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
          <g transform="translate(18, 20)">
            <path d="M0 5 C-3 2, -2 -2, 1 -3 C4 -1, 3 3, 0 5Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
        </svg>

        <!-- Bottom Left Corner Floral -->
        <svg class="gallery-floral gallery-floral--bl" viewBox="0 0 90 90" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <path d="M6 84 C 18 52, 42 24, 84 8" stroke="url(#goldFloraGradTL)" stroke-width="1.3" stroke-linecap="round"/>
          <path d="M32 54 C 20 42, 16 28, 22 16 C 26 24, 30 36, 36 44" stroke="url(#goldFloraGradTL)" stroke-width="0.9" fill="rgba(216, 200, 184, 0.2)"/>
          <path d="M50 36 C 42 22, 48 12, 58 14 C 58 22, 54 30, 50 36Z" fill="rgba(216, 200, 184, 0.25)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M22 66 C 10 68, 6 60, 10 52 C 16 56, 20 62, 22 66Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M68 20 C 72 8, 82 8, 84 14 C 80 20, 74 20, 68 20Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <g transform="translate(36, 38)">
            <path d="M-9 -3 C-10 -11, 4 -12, 8 -4 C12 4, -4 12, -9 -3Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-4 -8 C4 -12, 12 -4, 8 4 C3 10, -8 6, -4 -8Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-3 -2 C-3 -6, 3 -6, 3 -2 C3 2, -1 3, -1 1 C-1 0, 1 0, 1 -1" stroke="#8b4a52" stroke-width="0.9" fill="none" stroke-linecap="round"/>
            <circle cx="0" cy="0" r="2.2" fill="#e8b8be"/>
          </g>
          <g transform="translate(74, 12)">
            <path d="M0 6 C-4 2, -2 -3, 2 -4 C6 -2, 5 3, 0 6Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
          <g transform="translate(18, 20)">
            <path d="M0 5 C-3 2, -2 -2, 1 -3 C4 -1, 3 3, 0 5Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
        </svg>

        <!-- Bottom Right Corner Floral -->
        <svg class="gallery-floral gallery-floral--br" viewBox="0 0 90 90" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <path d="M6 84 C 18 52, 42 24, 84 8" stroke="url(#goldFloraGradTL)" stroke-width="1.3" stroke-linecap="round"/>
          <path d="M32 54 C 20 42, 16 28, 22 16 C 26 24, 30 36, 36 44" stroke="url(#goldFloraGradTL)" stroke-width="0.9" fill="rgba(216, 200, 184, 0.2)"/>
          <path d="M50 36 C 42 22, 48 12, 58 14 C 58 22, 54 30, 50 36Z" fill="rgba(216, 200, 184, 0.25)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M22 66 C 10 68, 6 60, 10 52 C 16 56, 20 62, 22 66Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <path d="M68 20 C 72 8, 82 8, 84 14 C 80 20, 74 20, 68 20Z" fill="rgba(216, 200, 184, 0.22)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          <g transform="translate(36, 38)">
            <path d="M-9 -3 C-10 -11, 4 -12, 8 -4 C12 4, -4 12, -9 -3Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-4 -8 C4 -12, 12 -4, 8 4 C3 10, -8 6, -4 -8Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
            <path d="M-3 -2 C-3 -6, 3 -6, 3 -2 C3 2, -1 3, -1 1 C-1 0, 1 0, 1 -1" stroke="#8b4a52" stroke-width="0.9" fill="none" stroke-linecap="round"/>
            <circle cx="0" cy="0" r="2.2" fill="#e8b8be"/>
          </g>
          <g transform="translate(74, 12)">
            <path d="M0 6 C-4 2, -2 -3, 2 -4 C6 -2, 5 3, 0 6Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
          <g transform="translate(18, 20)">
            <path d="M0 5 C-3 2, -2 -2, 1 -3 C4 -1, 3 3, 0 5Z" fill="url(#petalGlowTL)" stroke="url(#goldFloraGradTL)" stroke-width="0.8"/>
          </g>
        </svg>

        <!-- Floating Delicate Flowers on LEFT side -->
        <div class="gallery-flock gallery-flock--left" aria-hidden="true">
          <!-- Flower L1: Blooming Rose -->
          <div class="drifting-flower drifting-flower--l1">
            <svg class="flower-svg" viewBox="0 0 36 36" fill="none">
              <path d="M10 24 C 4 23, 2 17, 6 12 C 11 15, 12 21, 10 24 Z" fill="rgba(196, 175, 150, 0.55)" stroke="#bfa37e" stroke-width="0.6"/>
              <circle cx="18" cy="18" r="11" fill="rgba(252, 236, 238, 0.95)" stroke="#d4af37" stroke-width="0.8"/>
              <path d="M12 16 C 11 10, 19 9, 21 14 C 25 10, 28 16, 26 20 C 28 25, 22 28, 19 25 C 14 28, 10 23, 12 19 Z" fill="rgba(240, 198, 203, 0.92)" stroke="#c48b92" stroke-width="0.6"/>
              <path d="M15 17 C 15 14, 21 14, 21 17 C 21 20, 17 21, 17 19 C 17 18, 19 18, 19 17" stroke="#8b3a44" stroke-width="0.9" fill="none" stroke-linecap="round"/>
              <circle cx="18" cy="18" r="1.8" fill="#d4af37"/>
            </svg>
          </div>

          <!-- Flower L2: Rosebud with Stem -->
          <div class="drifting-flower drifting-flower--l2">
            <svg class="flower-svg" viewBox="0 0 32 32" fill="none">
              <path d="M8 28 C 12 24, 15 20, 18 16" stroke="#bfa37e" stroke-width="1.1" stroke-linecap="round"/>
              <path d="M12 22 C 8 20, 7 15, 10 13 C 13 16, 13 20, 12 22 Z" fill="rgba(196, 175, 150, 0.5)" stroke="#bfa37e" stroke-width="0.6"/>
              <path d="M16 18 C 14 12, 18 8, 23 9 C 27 10, 26 16, 21 19 Z" fill="rgba(242, 202, 207, 0.95)" stroke="#c48b92" stroke-width="0.7"/>
              <path d="M19 14 C 19 10, 23 9, 24 12" stroke="#d4af37" stroke-width="0.7" fill="none"/>
            </svg>
          </div>

          <!-- Flower L3: Floating Blossom -->
          <div class="drifting-flower drifting-flower--l3">
            <svg class="flower-svg" viewBox="0 0 28 28" fill="none">
              <circle cx="14" cy="14" r="8" fill="rgba(252, 238, 240, 0.95)" stroke="#d4af37" stroke-width="0.7"/>
              <path d="M8 12 C 8 7, 14 7, 16 11 C 20 7, 22 13, 20 17 C 21 21, 16 22, 14 20 C 11 22, 7 19, 8 15 Z" fill="rgba(235, 185, 192, 0.9)" stroke="#b86b74" stroke-width="0.5"/>
              <circle cx="14" cy="14" r="2" fill="#d4af37"/>
            </svg>
          </div>

          <!-- Flower L4: Soft Petals -->
          <div class="drifting-flower drifting-flower--l4">
            <svg class="flower-svg" viewBox="0 0 24 24" fill="none">
              <path d="M12 2 C 17 6, 20 12, 16 18 C 12 22, 5 20, 3 14 C 2 8, 7 3, 12 2 Z" fill="rgba(245, 210, 215, 0.92)" stroke="#d4af37" stroke-width="0.6"/>
              <path d="M12 5 C 13 10, 12 15, 8 18" stroke="rgba(255, 255, 255, 0.8)" stroke-width="0.6" fill="none"/>
            </svg>
          </div>

          <!-- Flower L5: Mini Bud -->
          <div class="drifting-flower drifting-flower--l5">
            <svg class="flower-svg" viewBox="0 0 26 26" fill="none">
              <path d="M13 14 C 11 9, 15 6, 19 7 C 22 8, 21 13, 17 15 Z" fill="rgba(242, 202, 207, 0.95)" stroke="#c48b92" stroke-width="0.6"/>
              <path d="M8 22 C 11 19, 13 16, 15 13" stroke="#bfa37e" stroke-width="0.9" stroke-linecap="round"/>
            </svg>
          </div>
        </div>

        <!-- Floating Delicate Flowers on RIGHT side -->
        <div class="gallery-flock gallery-flock--right" aria-hidden="true">
          <!-- Flower R1: Rosebud with Stem -->
          <div class="drifting-flower drifting-flower--r1">
            <svg class="flower-svg" viewBox="0 0 32 32" fill="none">
              <path d="M24 28 C 20 24, 17 20, 14 16" stroke="#bfa37e" stroke-width="1.1" stroke-linecap="round"/>
              <path d="M20 22 C 24 20, 25 15, 22 13 C 19 16, 19 20, 20 22 Z" fill="rgba(196, 175, 150, 0.5)" stroke="#bfa37e" stroke-width="0.6"/>
              <path d="M16 18 C 18 12, 14 8, 9 9 C 5 10, 6 16, 11 19 Z" fill="rgba(242, 202, 207, 0.95)" stroke="#c48b92" stroke-width="0.7"/>
              <path d="M13 14 C 13 10, 9 9, 8 12" stroke="#d4af37" stroke-width="0.7" fill="none"/>
            </svg>
          </div>

          <!-- Flower R2: Blooming Rose -->
          <div class="drifting-flower drifting-flower--r2">
            <svg class="flower-svg" viewBox="0 0 36 36" fill="none">
              <path d="M26 24 C 32 23, 34 17, 30 12 C 25 15, 24 21, 26 24 Z" fill="rgba(196, 175, 150, 0.55)" stroke="#bfa37e" stroke-width="0.6"/>
              <circle cx="18" cy="18" r="11" fill="rgba(252, 236, 238, 0.95)" stroke="#d4af37" stroke-width="0.8"/>
              <path d="M12 16 C 11 10, 19 9, 21 14 C 25 10, 28 16, 26 20 C 28 25, 22 28, 19 25 C 14 28, 10 23, 12 19 Z" fill="rgba(240, 198, 203, 0.92)" stroke="#c48b92" stroke-width="0.6"/>
              <path d="M15 17 C 15 14, 21 14, 21 17 C 21 20, 17 21, 17 19 C 17 18, 19 18, 19 17" stroke="#8b3a44" stroke-width="0.9" fill="none" stroke-linecap="round"/>
              <circle cx="18" cy="18" r="1.8" fill="#d4af37"/>
            </svg>
          </div>

          <!-- Flower R3: Soft Petals -->
          <div class="drifting-flower drifting-flower--r3">
            <svg class="flower-svg" viewBox="0 0 24 24" fill="none">
              <path d="M12 2 C 17 6, 20 12, 16 18 C 12 22, 5 20, 3 14 C 2 8, 7 3, 12 2 Z" fill="rgba(245, 210, 215, 0.92)" stroke="#d4af37" stroke-width="0.6"/>
              <path d="M12 5 C 13 10, 12 15, 8 18" stroke="rgba(255, 255, 255, 0.8)" stroke-width="0.6" fill="none"/>
            </svg>
          </div>

          <!-- Flower R4: Floating Blossom -->
          <div class="drifting-flower drifting-flower--r4">
            <svg class="flower-svg" viewBox="0 0 28 28" fill="none">
              <circle cx="14" cy="14" r="8" fill="rgba(252, 238, 240, 0.95)" stroke="#d4af37" stroke-width="0.7"/>
              <path d="M8 12 C 8 7, 14 7, 16 11 C 20 7, 22 13, 20 17 C 21 21, 16 22, 14 20 C 11 22, 7 19, 8 15 Z" fill="rgba(235, 185, 192, 0.9)" stroke="#b86b74" stroke-width="0.5"/>
              <circle cx="14" cy="14" r="2" fill="#d4af37"/>
            </svg>
          </div>

          <!-- Flower R5: Mini Bud -->
          <div class="drifting-flower drifting-flower--r5">
            <svg class="flower-svg" viewBox="0 0 26 26" fill="none">
              <path d="M13 14 C 15 9, 11 6, 7 7 C 4 8, 5 13, 9 15 Z" fill="rgba(242, 202, 207, 0.95)" stroke="#c48b92" stroke-width="0.6"/>
              <path d="M18 22 C 15 19, 13 16, 11 13" stroke="#bfa37e" stroke-width="0.9" stroke-linecap="round"/>
            </svg>
          </div>
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
import hand1Img from '@/assets/images/hand1.jpg'
import personImg from '@/assets/images/person.jpg'

const photos = [
  {
    src: deblaImg,
    tag: 'Blessing · دعاء وبركة',
    title: 'A Blessed Beginning',
    caption: 'على كتاب الله وسُنة رسوله، دعوات ترعى بداية حكايتنا — In faith and prayers, our journey begins',
  },
  {
    src: hand1Img,
    tag: 'Together · فرحة العمر',
    title: 'Bahaa & Eman',
    caption: 'ابتسامة العمر وفرحة تكتمل بكم.. معاً نحو غدٍ أجمل — Two hearts radiating love and everlasting joy',
  },
  {
    src: personImg,
    tag: 'The Rings · عهد المحبة',
    title: 'اليوم وغدًا وإلى الأبد',
    caption: 'رمز العهد والميثاق وتاريخ محفور في الوجدان (14/8/2026) — Today, tomorrow, and forever together',
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

function petalStyle(p) {
  const lefts = [6, 88, 12, 85, 4, 92]
  const tops = [14, 22, 58, 72, 42, 86]
  const delays = [0, 1.8, 3.2, 0.9, 2.4, 4.1]
  const durations = [6.5, 7.2, 8, 6.8, 7.5, 8.5]
  const scales = [0.85, 1.1, 0.75, 1, 0.9, 0.8]
  return {
    left: `${lefts[(p - 1) % lefts.length]}%`,
    top: `${tops[(p - 1) % tops.length]}%`,
    animationDelay: `${delays[(p - 1) % delays.length]}s`,
    animationDuration: `${durations[(p - 1) % durations.length]}s`,
    transform: `scale(${scales[(p - 1) % scales.length]})`,
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

/* ── Floating Flower Petals ── */
.gallery-petals {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
  overflow: hidden;
}

.gallery-petal {
  position: absolute;
  animation: petalSwayFloat ease-in-out infinite alternate;
  opacity: 0.65;
  filter: drop-shadow(0 2px 4px rgba(74, 20, 26, 0.1));
}

@keyframes petalSwayFloat {
  0% {
    transform: translateY(0) rotate(0deg);
    opacity: 0.35;
  }
  50% {
    opacity: 0.75;
  }
  100% {
    transform: translateY(-24px) rotate(25deg);
    opacity: 0.4;
  }
}

/* ── Card Wrapper & Delicate Corner Florals ── */
.gallery-card-wrapper {
  position: relative;
  max-width: 420px;
  margin: 0 auto;
}

.gallery-floral {
  position: absolute;
  width: 66px;
  height: 66px;
  pointer-events: none;
  z-index: 20;
  filter: drop-shadow(0 3px 8px rgba(74, 20, 26, 0.28));
  transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.gallery-floral--tl {
  top: -14px;
  left: -14px;
}

.gallery-floral--tr {
  top: -14px;
  right: -14px;
  transform: scaleX(-1);
}

.gallery-floral--bl {
  bottom: -14px;
  left: -14px;
  transform: scaleY(-1);
}

.gallery-floral--br {
  bottom: -14px;
  right: -14px;
  transform: scale(-1);
}

.gallery-card-wrapper:hover .gallery-floral--tl {
  transform: scale(1.08) rotate(-3deg);
}

.gallery-card-wrapper:hover .gallery-floral--tr {
  transform: scaleX(-1) scale(1.08) rotate(3deg);
}

.gallery-card-wrapper:hover .gallery-floral--bl {
  transform: scaleY(-1) scale(1.08) rotate(3deg);
}

.gallery-card-wrapper:hover .gallery-floral--br {
  transform: scale(-1) scale(1.08) rotate(-3deg);
}

/* ── Side Drifting Flowers (الأجناب) ── */
.gallery-flock {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 48px;
  pointer-events: none;
  z-index: 25;
}

.gallery-flock--left {
  left: -22px;
}

.gallery-flock--right {
  right: -22px;
}

@media (min-width: 480px) {
  .gallery-flock--left {
    left: -40px;
    width: 56px;
  }
  .gallery-flock--right {
    right: -40px;
    width: 56px;
  }
}

.drifting-flower {
  position: absolute;
  filter: drop-shadow(0 3px 6px rgba(74, 20, 26, 0.24));
  transition: transform 0.4s ease;
}

.flower-svg {
  display: block;
  width: 100%;
  height: 100%;
}

/* Left Side Flower Placements */
.drifting-flower--l1 {
  top: 8%;
  left: 6px;
  width: 32px;
  height: 32px;
  animation: floatDrift1 5.2s ease-in-out infinite alternate;
}

.drifting-flower--l2 {
  top: 28%;
  left: -4px;
  width: 28px;
  height: 28px;
  animation: floatDrift2 6s ease-in-out infinite alternate 0.8s;
}

.drifting-flower--l3 {
  top: 49%;
  left: 8px;
  width: 26px;
  height: 26px;
  animation: floatDrift3 5.5s ease-in-out infinite alternate 1.6s;
}

.drifting-flower--l4 {
  top: 69%;
  left: -2px;
  width: 24px;
  height: 24px;
  animation: floatDrift1 6.3s ease-in-out infinite alternate 2.4s;
}

.drifting-flower--l5 {
  top: 88%;
  left: 6px;
  width: 27px;
  height: 27px;
  animation: floatDrift2 5.8s ease-in-out infinite alternate 1.2s;
}

/* Right Side Flower Placements */
.drifting-flower--r1 {
  top: 12%;
  right: -4px;
  width: 28px;
  height: 28px;
  animation: floatDrift2 5.6s ease-in-out infinite alternate 0.5s;
}

.drifting-flower--r2 {
  top: 32%;
  right: 6px;
  width: 33px;
  height: 33px;
  animation: floatDrift1 5s ease-in-out infinite alternate 1.4s;
}

.drifting-flower--r3 {
  top: 52%;
  right: -6px;
  width: 24px;
  height: 24px;
  animation: floatDrift3 6.2s ease-in-out infinite alternate 2s;
}

.drifting-flower--r4 {
  top: 72%;
  right: 8px;
  width: 27px;
  height: 27px;
  animation: floatDrift2 5.4s ease-in-out infinite alternate 0.9s;
}

.drifting-flower--r5 {
  top: 89%;
  right: -2px;
  width: 28px;
  height: 28px;
  animation: floatDrift1 6s ease-in-out infinite alternate 2.7s;
}

@keyframes floatDrift1 {
  0%   { transform: translateY(0) translateX(0) rotate(0deg) scale(1); }
  50%  { transform: translateY(-12px) translateX(4px) rotate(8deg) scale(1.05); }
  100% { transform: translateY(-22px) translateX(-3px) rotate(-6deg) scale(0.98); }
}

@keyframes floatDrift2 {
  0%   { transform: translateY(0) translateX(0) rotate(0deg) scale(0.96); }
  50%  { transform: translateY(-15px) translateX(-5px) rotate(-10deg) scale(1.04); }
  100% { transform: translateY(-26px) translateX(3px) rotate(7deg) scale(1); }
}

@keyframes floatDrift3 {
  0%   { transform: translateY(0) translateX(0) rotate(0deg) scale(1); }
  50%  { transform: translateY(-13px) translateX(6px) rotate(12deg) scale(1.06); }
  100% { transform: translateY(-24px) translateX(-4px) rotate(-8deg) scale(0.97); }
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
  grid-template-columns: repeat(3, 1fr);
  gap: 0.65rem;
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
