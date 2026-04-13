<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const infoCol = ref(null)
</script>

<template>
  <!-- ── Atmospheric background layers ── -->
  <div class="bg-grid" aria-hidden="true"></div>
  <div class="bg-fog" aria-hidden="true"></div>
  <div class="bg-fog-2" aria-hidden="true"></div>
  <div class="bg-arcadia" aria-hidden="true"></div>
  <div class="bg-vignette" aria-hidden="true"></div>
  <div class="scanline" aria-hidden="true"></div>
  <div class="lightning" aria-hidden="true"></div>

  <!-- Constellation overlay (Arcadia sky) -->
  <div class="constellation" aria-hidden="true">
    <span v-for="i in 55" :key="'star'+i" class="star" :style="{ '--i': i }"></span>
  </div>

  <!-- Hellgate portal glow at bottom -->
  <div class="hellgate" aria-hidden="true"></div>

  <!-- Newport waterline (The Longest Journey) -->
  <div class="waterline" aria-hidden="true"></div>

  <!-- Screen corner ornaments -->
  <div class="corner-ornament tl" aria-hidden="true"></div>
  <div class="corner-ornament tr" aria-hidden="true"></div>
  <div class="corner-ornament bl" aria-hidden="true"></div>
  <div class="corner-ornament br" aria-hidden="true"></div>

  <!-- Blood drips from top edge -->
  <div class="blood-drips" aria-hidden="true">
    <span v-for="i in 18" :key="'drip'+i" class="blood-drip" :style="{ '--i': i }"></span>
  </div>

  <!-- Ember particles -->
  <div class="embers" aria-hidden="true">
    <span v-for="i in 30" :key="i" class="ember" :style="{ '--i': i }"></span>
  </div>

  <!-- Soul wisps -->
  <div class="wisps" aria-hidden="true">
    <span v-for="i in 9" :key="'wisp'+i" class="wisp" :style="{ '--i': i }"></span>
  </div>

  <header class="hero">
    <div class="avatar-col">
      <div class="hex-frame">
        <div class="hex-orbit-ring"></div>
        <img alt="Kacper" class="avatar-img" src="./assets/kacper.jpg" />
      </div>
      <div class="online-badge">
        <span class="pulse-dot"></span>
        ONLINE
      </div>
    </div>

    <div class="info-col side-animation" ref="infoCol">
      <HelloWorld msg="Kacper Rybczyński" :card-el="infoCol" />
    </div>
  </header>

  <main>
    <!-- Gothic separator -->
    <div class="gothic-sep" aria-hidden="true">
      <span class="sep-line"></span>
      <span class="sep-glyph">⛧ ⚖ ⛧</span>
      <span class="sep-line"></span>
    </div>

    <section class="quotes">
      <p>"First rule of business, protect your investment."</p>
      <p class="attr">— Etiquette of the Banker, 1775</p>
      <p>"The only way to get smarter is by playing a smarter opponent."</p>
      <p class="attr">— Fundamentals of Chess, 1883</p>
    </section>

    <div class="symbol-wrapper">
      <div class="sym-ring outer-sym-ring"></div>
      <div class="sym-ring inner-sym-ring"></div>
      <div class="output">
        <div class="smoki"></div>
        <div class="rownowaga"></div>
      </div>
    </div>

    <div class="cypher">
      <div class="xtext"></div>
    </div>
  </main>
</template>

<style scoped>
@font-face {
  font-family: "Exocet Blizzard Light";
  src: url('./assets/exocet-blizzard-light.ttf');
}

/* ── Background grid ────────────────────────────── */
.bg-grid {
  position: fixed;
  inset: 0;
  z-index: 0;
  background-image:
    linear-gradient(rgba(155, 0, 0, 0.07) 1px, transparent 1px),
    linear-gradient(90deg, rgba(155, 0, 0, 0.07) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events: none;
}

/* ── Primary blood fog ──────────────────────────── */
.bg-fog {
  position: fixed;
  inset: 0;
  z-index: 0;
  background:
    radial-gradient(ellipse at 15% 85%, rgba(130, 0, 0, 0.50) 0%, transparent 55%),
    radial-gradient(ellipse at 85% 15%, rgba(95, 0, 0, 0.38) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 100%, rgba(150, 0, 0, 0.55) 0%, transparent 45%),
    radial-gradient(ellipse at 0% 50%,  rgba(70,  0, 0, 0.28) 0%, transparent 40%);
  pointer-events: none;
  animation: fog-breathe 18s ease-in-out infinite alternate;
}

/* ── Secondary void fog ─────────────────────────── */
.bg-fog-2 {
  position: fixed;
  inset: 0;
  z-index: 0;
  background:
    radial-gradient(ellipse at 72% 68%, rgba(80, 0, 55, 0.22) 0%, transparent 45%),
    radial-gradient(ellipse at 28% 22%, rgba(55, 0,  0, 0.22) 0%, transparent 42%),
    radial-gradient(ellipse at 55% 45%, rgba(40, 0, 30, 0.14) 0%, transparent 35%);
  pointer-events: none;
  animation: fog-breathe 28s ease-in-out infinite alternate-reverse;
}

/* ── Arcadia haze (The Longest Journey — bleeds from the left) ── */
.bg-arcadia {
  position: fixed;
  inset: 0;
  z-index: 0;
  background:
    radial-gradient(ellipse at 0% 40%,  rgba(13, 74, 92, 0.28) 0%, transparent 48%),
    radial-gradient(ellipse at 8%  72%,  rgba(30, 92, 68, 0.18) 0%, transparent 40%),
    radial-gradient(ellipse at 20% 15%,  rgba(10, 42, 58, 0.20) 0%, transparent 38%);
  pointer-events: none;
  animation: arcadia-breathe 32s ease-in-out infinite alternate;
}

@keyframes arcadia-breathe {
  0%   { opacity: 0.45; transform: scale(1);    }
  50%  { opacity: 0.85; transform: scale(1.05); }
  100% { opacity: 0.40; transform: scale(0.97); }
}

@keyframes fog-breathe {
  0%   { opacity: 0.55; transform: scale(1);    }
  50%  { opacity: 1;    transform: scale(1.07); }
  100% { opacity: 0.50; transform: scale(0.95); }
}

/* ── Constellation — Arcadia sky ────────────────── */
.constellation {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  overflow: hidden;
}

.star {
  position: absolute;
  border-radius: 50%;
  /* Spread across the full viewport using prime-ish offsets */
  top:  calc((var(--i) * 37 % 97) * 1%);
  left: calc((var(--i) * 53 % 97) * 1%);
  width:  calc(1px + (var(--i) % 2) * 1px);
  height: calc(1px + (var(--i) % 2) * 1px);
  /* Even-indexed stars → teal/arcadia, odd → faint gold */
  background: color-mix(in srgb,
    rgba(0, 180, 140, 0.9) calc((var(--i) % 2) * 100%),
    rgba(200, 160, 80, 0.7) calc((1 - var(--i) % 2) * 100%)
  );
  box-shadow: 0 0 3px 1px color-mix(in srgb,
    rgba(0, 150, 120, 0.35) calc((var(--i) % 2) * 100%),
    rgba(200, 140, 30, 0.25) calc((1 - var(--i) % 2) * 100%)
  );
  animation: star-pulse calc(3s + (var(--i) % 7) * 0.8s) ease-in-out calc(var(--i) * 0.33s) infinite alternate;
}

@keyframes star-pulse {
  0%   { opacity: 0.15; }
  50%  { opacity: 0.75; }
  100% { opacity: 0.20; }
}

/* ── Newport waterline (The Longest Journey) ──── */
.waterline {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 28px;
  z-index: 0;
  pointer-events: none;
  background:
    repeating-linear-gradient(
      90deg,
      transparent 0px,
      rgba(13, 74, 92, 0.18) 60px,
      rgba(30, 92, 68, 0.12) 90px,
      rgba(10, 42, 58, 0.20) 130px,
      transparent 180px
    );
  animation: water-shimmer 9s ease-in-out infinite alternate;
  mask-image: linear-gradient(to top, rgba(0,0,0,0.6) 0%, transparent 100%);
  -webkit-mask-image: linear-gradient(to top, rgba(0,0,0,0.6) 0%, transparent 100%);
}

@keyframes water-shimmer {
  0%   { background-position: 0 0;     opacity: 0.55; }
  50%  { background-position: 40px 0;  opacity: 0.85; }
  100% { background-position: -30px 0; opacity: 0.60; }
}

/* ── Vignette ───────────────────────────────────── */
.bg-vignette {
  position: fixed;
  inset: 0;
  z-index: 0;
  background: radial-gradient(ellipse at center, transparent 20%, rgba(0, 0, 0, 0.94) 100%);
  pointer-events: none;
}

/* ── Scanlines ──────────────────────────────────── */
.scanline {
  position: fixed;
  inset: 0;
  z-index: 0;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0px,
    transparent 2px,
    rgba(0, 0, 0, 0.18) 2px,
    rgba(0, 0, 0, 0.18) 3px
  );
  pointer-events: none;
  animation: scanmove 6s linear infinite;
}

@keyframes scanmove {
  0%   { background-position: 0 0;    }
  100% { background-position: 0 80px; }
}

/* ── Lightning flash ────────────────────────────── */
.lightning {
  position: fixed;
  inset: 0;
  z-index: 0;
  background: rgba(180, 0, 0, 0.12);
  pointer-events: none;
  opacity: 0;
  animation: lightning-flash 17s ease-in-out infinite;
}

@keyframes lightning-flash {
  0%, 86%, 89.5%, 91%, 100% { opacity: 0; }
  87%   { opacity: 1;   }
  88%   { opacity: 0;   }
  90%   { opacity: 0.5; }
}

/* ── Hellgate portal ────────────────────────────── */
.hellgate {
  position: fixed;
  bottom: -60px;
  left: 50%;
  width: 140%;
  height: 300px;
  z-index: 0;
  pointer-events: none;
  background: radial-gradient(ellipse at 50% 100%,
    rgba(210, 0, 0, 0.40) 0%,
    rgba(110, 0, 0, 0.28) 22%,
    rgba(45,  0, 0, 0.16) 48%,
    transparent 68%
  );
  transform: translateX(-50%);
  animation: hellgate-pulse 7s ease-in-out infinite alternate;
}

@keyframes hellgate-pulse {
  0%   { opacity: 0.45; transform: translateX(-50%) scaleX(0.93); }
  100% { opacity: 1.00; transform: translateX(-50%) scaleX(1.07); }
}

/* ── Corner ornaments ───────────────────────────── */
.corner-ornament {
  position: fixed;
  width: 72px;
  height: 72px;
  z-index: 2;
  pointer-events: none;
}

.corner-ornament.tl { top: 14px;    left: 14px;  border-top: 1px solid rgba(155,0,0,0.50); border-left:  1px solid rgba(155,0,0,0.50); }
.corner-ornament.tr { top: 14px;    right: 14px; border-top: 1px solid rgba(155,0,0,0.50); border-right: 1px solid rgba(155,0,0,0.50); }
.corner-ornament.bl { bottom: 14px; left: 14px;  border-bottom: 1px solid rgba(155,0,0,0.50); border-left:  1px solid rgba(155,0,0,0.50); }
.corner-ornament.br { bottom: 14px; right: 14px; border-bottom: 1px solid rgba(155,0,0,0.50); border-right: 1px solid rgba(155,0,0,0.50); }

.corner-ornament::before {
  content: "◆";
  position: absolute;
  font-size: 0.48rem;
  color: rgba(155, 0, 0, 0.65);
  text-shadow: 0 0 8px rgba(155, 0, 0, 0.8);
  animation: corner-glow 4s ease-in-out infinite;
}
.corner-ornament.tl::before { top: -5px;    left: -4px;  }
.corner-ornament.tr::before { top: -5px;    right: -4px; }
.corner-ornament.bl::before { bottom: -5px; left: -4px;  }
.corner-ornament.br::before { bottom: -5px; right: -4px; }

.corner-ornament::after {
  content: "";
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: rgba(155, 0, 0, 0.4);
  box-shadow: 0 0 8px 2px rgba(155, 0, 0, 0.3);
  animation: corner-glow 4s ease-in-out infinite alternate;
}
.corner-ornament.tl::after { bottom: 0; right: 0; }
.corner-ornament.tr::after { bottom: 0; left:  0; }
.corner-ornament.bl::after { top:    0; right: 0; }
.corner-ornament.br::after { top:    0; left:  0; }

@keyframes corner-glow {
  0%, 100% { opacity: 0.5; }
  50%       { opacity: 1;   }
}

/* ── Blood drips ────────────────────────────────── */
.blood-drips {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 160px;
  z-index: 1;
  pointer-events: none;
  overflow: hidden;
}

.blood-drip {
  position: absolute;
  top: 0;
  left: calc(var(--i) * 5.5% + 0.5%);
  width: 2px;
  border-radius: 0 0 60% 60%;
  background: linear-gradient(to bottom, rgba(130, 0, 0, 0.9), rgba(180, 0, 0, 0.3), rgba(160, 0, 0, 0));
  animation: drip calc(2.4s + var(--i) * 0.28s) ease-in calc(var(--i) * 0.95s) infinite;
}

@keyframes drip {
  0%   { height: 4px;   opacity: 0.9; }
  25%  { height: 35px;  opacity: 0.75; }
  60%  { height: 85px;  opacity: 0.5;  }
  100% { height: 130px; opacity: 0;    }
}

/* ── Ember particles ────────────────────────────── */
.embers {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  overflow: hidden;
}

.ember {
  position: absolute;
  bottom: -6px;
  left: calc(var(--i) * 3.4% - 1.7%);
  width: 2px;
  height: 2px;
  border-radius: 50%;
  background: radial-gradient(circle, #FF8800 0%, #8B0000 100%);
  box-shadow: 0 0 5px 2px rgba(200, 75, 0, 0.55);
  animation: ember-rise calc(4.2s + var(--i) * 0.22s) ease-out calc(var(--i) * 0.42s) infinite;
}

@keyframes ember-rise {
  0%   { transform: translateY(0)      translateX(0);     opacity: 0.9; width: 2px; height: 2px; }
  25%  { transform: translateY(-65px)  translateX(9px);   opacity: 0.7; }
  55%  { transform: translateY(-140px) translateX(-7px);  opacity: 0.4; width: 1px; height: 1px; }
  100% { transform: translateY(-250px) translateX(12px);  opacity: 0;   width: 1px; height: 1px; }
}

/* ── Soul wisps ─────────────────────────────────── */
.wisps {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  overflow: hidden;
}

.wisp {
  position: absolute;
  bottom: 15%;
  left: calc(var(--i) * 11% - 3%);
  width: 3px;
  height: 3px;
  border-radius: 50%;
  /* odd wisps → D2 amber soul fire */
  background: rgba(200, 120, 30, 0.92);
  box-shadow:
    0 0 6px  3px rgba(180, 90,  0,  0.55),
    0 0 14px 6px rgba(140, 40,  0,  0.22);
  animation: wisp-float calc(10s + var(--i) * 0.7s) ease-in-out calc(var(--i) * 1.6s) infinite;
}

/* even wisps → TLJ Arcadia shift magic (teal) */
.wisp:nth-child(even) {
  background: rgba(0, 180, 140, 0.92);
  box-shadow:
    0 0 6px  3px rgba(0,  150, 110, 0.55),
    0 0 14px 6px rgba(0,   80,  70, 0.22);
}

@keyframes wisp-float {
  0%   { transform: translateY(0)      translateX(0);     opacity: 0;    }
  8%   { opacity: 0.75; }
  35%  { transform: translateY(-90px)  translateX(22px);  opacity: 0.6;  }
  65%  { transform: translateY(-210px) translateX(-16px); opacity: 0.35; }
  100% { transform: translateY(-400px) translateX(28px);  opacity: 0;    }
}

/* ── Hero layout ────────────────────────────────── */
header.hero {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2.5rem;
  padding-top: 3rem;
}

@media (min-width: 1024px) {
  header.hero {
    flex-direction: row;
    align-items: flex-start;
    gap: 4rem;
    padding-top: 0;
  }
}

/* ── Avatar ─────────────────────────────────────── */
.avatar-col {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
  flex-shrink: 0;
}

.hex-frame {
  position: relative;
  width: 168px;
  height: 168px;
}

.avatar-img {
  width: 168px;
  height: 168px;
  object-fit: cover;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  display: block;
  filter: contrast(1.12) brightness(0.86) saturate(0.88);
  transition: filter 0.4s;
}

.hex-frame:hover .avatar-img {
  filter: contrast(1.2) brightness(0.96) saturate(1.1);
}

/* Hex border glow — world-shift gradient (D2 hellfire → Arcadia teal) */
.hex-frame::after {
  content: "";
  position: absolute;
  inset: -4px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: linear-gradient(135deg,
    #9B0000 0%,
    #3A0000 28%,
    #C8960C 50%,
    #0A4A5C 76%,
    #1E5C44 100%
  );
  z-index: -1;
  animation: frame-pulse 3s ease-in-out infinite;
}

@keyframes frame-pulse {
  0%, 100% { opacity: 0.7; }
  50%       { opacity: 1; filter: drop-shadow(0 0 14px rgba(155, 0, 0, 0.75)); }
}

/* Orbit ring around hex */
.hex-orbit-ring {
  position: absolute;
  width: 222px;
  height: 222px;
  top: 50%;
  left: 50%;
  margin-top: -111px;
  margin-left: -111px;
  border-radius: 50%;
  border: 1px dashed rgba(155, 0, 0, 0.32);
  box-shadow: 0 0 12px rgba(155, 0, 0, 0.12), inset 0 0 12px rgba(155, 0, 0, 0.06);
  animation: orbit-spin 22s linear infinite;
  pointer-events: none;
}

.hex-orbit-ring::before {
  content: "";
  position: absolute;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: radial-gradient(circle, #FF5500, #8B0000);
  box-shadow: 0 0 12px 4px rgba(155, 0, 0, 0.6);
  top: -4px;
  left: 50%;
  margin-left: -3.5px;
}

.hex-orbit-ring::after {
  content: "";
  position: absolute;
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: radial-gradient(circle, #C8960C, #5A3A00);
  box-shadow: 0 0 10px 3px rgba(200, 150, 12, 0.5);
  bottom: -3px;
  left: 50%;
  margin-left: -2.5px;
}

@keyframes orbit-spin {
  to { transform: rotate(360deg); }
}

/* ── Online badge ───────────────────────────────── */
.online-badge {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  color: #9B0000;
  border: 1px solid rgba(155, 0, 0, 0.45);
  padding: 0.2rem 0.75rem;
  clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
  background: rgba(155, 0, 0, 0.09);
  text-shadow: 0 0 10px rgba(155, 0, 0, 0.8);
}

.pulse-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #9B0000;
  box-shadow: 0 0 8px rgba(155, 0, 0, 0.9);
  animation: blink 1.4s ease-in-out infinite;
  flex-shrink: 0;
}

@keyframes blink {
  0%, 100% { opacity: 1;    }
  50%       { opacity: 0.12; }
}

/* ── Side glow line ─────────────────────────────── */
.side-animation {
  flex: 1;
  position: relative;
  transition: transform 0.18s;
}

.side-animation::after {
  content: "";
  height: 160px;
  width: 2px;
  position: absolute;
  right: 0;
  top: var(--slide-top, 65%);
  opacity: var(--slide-opacity, 0);
  transition: top 400ms ease, opacity 400ms ease;
  background: linear-gradient(transparent, #8B0000, transparent);
  box-shadow: 0 0 14px rgba(155, 0, 0, 0.55);
}

.side-animation:hover::after {
  top: 25%;
  opacity: 1;
}

/* ── Gothic separator ───────────────────────────── */
.gothic-sep {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  margin: 0.5rem 0 1rem;
  position: relative;
  z-index: 1;
}

.sep-line {
  flex: 1;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(155, 0, 0, 0.55),
    rgba(200, 150, 12, 0.35),
    rgba(155, 0, 0, 0.55),
    transparent
  );
  box-shadow: 0 0 5px rgba(155, 0, 0, 0.2);
}

.sep-glyph {
  color: rgba(155, 0, 0, 0.75);
  font-size: 0.95rem;
  letter-spacing: 0.55em;
  animation: glyph-pulse 4s ease-in-out infinite;
}

@keyframes glyph-pulse {
  0%, 100% { opacity: 0.55; text-shadow: 0 0 10px rgba(155, 0, 0, 0.5); }
  50%       { opacity: 1;    text-shadow: 0 0 22px rgba(155, 0, 0, 0.95), 0 0 44px rgba(155, 0, 0, 0.35); }
}

/* ── Quotes ─────────────────────────────────────── */
.quotes {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  margin-bottom: 2rem;
  position: relative;
  z-index: 1;
  border: 1px solid rgba(155, 0, 0, 0.22);
  background: linear-gradient(135deg, rgba(28, 0, 0, 0.42) 0%, rgba(8, 0, 0, 0.58) 100%);
  padding: 1.1rem 1.3rem;
  clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
}

.quotes::before {
  content: "⛧";
  position: absolute;
  top: -0.75rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 1rem;
  color: rgba(155, 0, 0, 0.7);
  background: var(--color-background);
  padding: 0 0.5rem;
  text-shadow: 0 0 14px rgba(155, 0, 0, 0.8);
}

.quotes p {
  font-size: 0.88rem;
  color: rgba(200, 168, 112, 0.52);
}

.quotes .attr {
  color: rgba(200, 150, 12, 0.62);
  margin-bottom: 0.75rem;
  font-size: 0.78rem;
  letter-spacing: 0.04em;
}

/* ── Symbol section ─────────────────────────────── */
.symbol-wrapper {
  display: grid;
  place-items: center;
  margin-bottom: 1rem;
  position: relative;
  z-index: 1;
  height: 256px;
}

/* Rotating rune rings */
.sym-ring {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  top: 50%;
  left: 50%;
}

/* outer ring — D2 hellfire */
.outer-sym-ring {
  width: 336px;
  height: 336px;
  margin-top: -168px;
  margin-left: -168px;
  border: 1px dashed rgba(155, 0, 0, 0.30);
  box-shadow:
    0 0 24px rgba(155, 0, 0, 0.10),
    inset 0 0 24px rgba(155, 0, 0, 0.05);
  animation: spin-ring-cw 38s linear infinite;
}

/* inner ring — TLJ Arcadia (teal, opposite spin) */
.inner-sym-ring {
  width: 290px;
  height: 290px;
  margin-top: -145px;
  margin-left: -145px;
  border: 1px solid rgba(13, 74, 92, 0.38);
  box-shadow:
    0 0 18px rgba(13, 74, 92, 0.10),
    inset 0 0 18px rgba(0, 130, 100, 0.06);
  animation: spin-ring-ccw 26s linear infinite;
}

@keyframes spin-ring-cw  { to { transform: rotate(360deg);   } }
@keyframes spin-ring-ccw { to { transform: rotate(-360deg);  } }

.smoki {
  background-image: url("./assets/smoki.png");
  width: 257px;
  height: 256px;
  animation: spin 12s linear infinite;
  z-index: 1;
  position: absolute;
  filter: sepia(1) saturate(7) hue-rotate(310deg) brightness(0.70);
}

.rownowaga {
  background-image: url("./assets/rownowaga.png");
  width: 257px;
  height: 256px;
  z-index: 2;
  position: relative;
  filter: sepia(1) saturate(5) hue-rotate(15deg) brightness(0.72);
}

.output {
  width: 256px;
  height: 256px;
}

@keyframes spin {
  to { transform: rotate(-360deg); }
}

/* ── Cypher text ────────────────────────────────── */
.cypher {
  justify-content: center;
  align-items: center;
  display: flex;
  margin-top: 10px;
  position: relative;
  z-index: 1;
}
</style>
