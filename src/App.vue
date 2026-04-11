<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const infoCol = ref(null)
</script>

<template>
  <!-- Atmospheric background layers -->
  <div class="bg-grid" aria-hidden="true"></div>
  <div class="bg-fog" aria-hidden="true"></div>
  <div class="bg-vignette" aria-hidden="true"></div>
  <div class="scanline" aria-hidden="true"></div>

  <!-- Ember particles -->
  <div class="embers" aria-hidden="true">
    <span v-for="i in 14" :key="i" class="ember" :style="{ '--i': i }"></span>
  </div>

  <header class="hero">
    <div class="avatar-col">
      <div class="hex-frame">
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
      <span class="sep-glyph">◆ ◆ ◆</span>
      <span class="sep-line"></span>
    </div>

    <section class="quotes">
      <p>"First rule of business, protect your investment."</p>
      <p class="attr">— Etiquette of the Banker, 1775</p>
      <p>"The only way to get smarter is by playing a smarter opponent."</p>
      <p class="attr">— Fundamentals of Chess, 1883</p>
    </section>

    <div class="symbol-wrapper">
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
    linear-gradient(rgba(155, 0, 0, 0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(155, 0, 0, 0.04) 1px, transparent 1px);
  background-size: 48px 48px;
  pointer-events: none;
}

/* ── Blood fog overlay ──────────────────────────── */
.bg-fog {
  position: fixed;
  inset: 0;
  z-index: 0;
  background:
    radial-gradient(ellipse at 15% 85%, rgba(100, 0, 0, 0.35) 0%, transparent 55%),
    radial-gradient(ellipse at 85% 15%, rgba(80, 0, 0, 0.25) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 100%, rgba(120, 0, 0, 0.4) 0%, transparent 45%),
    radial-gradient(ellipse at 0% 50%, rgba(60, 0, 0, 0.2) 0%, transparent 40%);
  pointer-events: none;
  animation: fog-breathe 18s ease-in-out infinite alternate;
}

@keyframes fog-breathe {
  0%   { opacity: 0.7; transform: scale(1); }
  50%  { opacity: 1;   transform: scale(1.04); }
  100% { opacity: 0.65; transform: scale(0.97); }
}

/* ── Vignette ───────────────────────────────────── */
.bg-vignette {
  position: fixed;
  inset: 0;
  z-index: 0;
  background: radial-gradient(ellipse at center, transparent 35%, rgba(0, 0, 0, 0.85) 100%);
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
    transparent 3px,
    rgba(0, 0, 0, 0.12) 3px,
    rgba(0, 0, 0, 0.12) 4px
  );
  pointer-events: none;
  animation: scanmove 8s linear infinite;
}

@keyframes scanmove {
  0%   { background-position: 0 0; }
  100% { background-position: 0 100px; }
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
  left: calc(var(--i) * 7.1% - 3.5%);
  width: 2px;
  height: 2px;
  border-radius: 50%;
  background: radial-gradient(circle, #FF7B00 0%, #8B0000 100%);
  box-shadow: 0 0 5px 2px rgba(200, 75, 0, 0.55);
  animation:
    ember-rise calc(4.5s + var(--i) * 0.28s) ease-out calc(var(--i) * 0.55s) infinite;
}

@keyframes ember-rise {
  0%   { transform: translateY(0)     translateX(0);     opacity: 0.9; width: 2px; height: 2px; }
  25%  { transform: translateY(-60px) translateX(8px);   opacity: 0.7; }
  55%  { transform: translateY(-130px) translateX(-6px); opacity: 0.4; width: 1px; height: 1px; }
  100% { transform: translateY(-220px) translateX(10px); opacity: 0;   width: 1px; height: 1px; }
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
  filter: contrast(1.05) brightness(0.92);
}

/* Hex border glow */
.hex-frame::after {
  content: "";
  position: absolute;
  inset: -4px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: linear-gradient(135deg, #8B0000 0%, #3A0000 45%, #C8960C 100%);
  z-index: -1;
  animation: frame-pulse 3s ease-in-out infinite;
}

@keyframes frame-pulse {
  0%, 100% { opacity: 0.65; }
  50%       { opacity: 1; filter: drop-shadow(0 0 8px rgba(155, 0, 0, 0.6)); }
}

/* ── Online badge ───────────────────────────────── */
.online-badge {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  color: #9B0000;
  border: 1px solid rgba(155, 0, 0, 0.4);
  padding: 0.2rem 0.75rem;
  clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
  background: rgba(155, 0, 0, 0.08);
  text-shadow: 0 0 10px rgba(155, 0, 0, 0.7);
}

.pulse-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #9B0000;
  box-shadow: 0 0 6px rgba(155, 0, 0, 0.8);
  animation: blink 1.4s ease-in-out infinite;
  flex-shrink: 0;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.15; }
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
  box-shadow: 0 0 12px rgba(155, 0, 0, 0.5);
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
  background: linear-gradient(90deg, transparent, rgba(155, 0, 0, 0.5), transparent);
}

.sep-glyph {
  color: rgba(155, 0, 0, 0.55);
  font-size: 0.55rem;
  letter-spacing: 0.4em;
}

/* ── Quotes ─────────────────────────────────────── */
.quotes {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  margin-bottom: 2rem;
  position: relative;
  z-index: 1;
}

.quotes p {
  font-size: 0.88rem;
  color: rgba(200, 168, 112, 0.45);
}

.quotes .attr {
  color: rgba(200, 150, 12, 0.55);
  margin-bottom: 0.75rem;
  font-size: 0.78rem;
  letter-spacing: 0.04em;
}

/* ── Symbol ─────────────────────────────────────── */
.symbol-wrapper {
  display: grid;
  place-items: center;
  margin-bottom: 1rem;
  position: relative;
  z-index: 1;
}

.smoki {
  background-image: url("./assets/smoki.png");
  width: 257px;
  height: 256px;
  animation: spin 12s linear infinite;
  z-index: 1;
  position: absolute;
  filter: sepia(1) saturate(6) hue-rotate(310deg) brightness(0.65);
}

.rownowaga {
  background-image: url("./assets/rownowaga.png");
  width: 257px;
  height: 256px;
  z-index: 2;
  position: relative;
  filter: sepia(1) saturate(4) hue-rotate(15deg) brightness(0.7);
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
