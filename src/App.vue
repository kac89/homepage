<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const infoCol = ref(null)
</script>

<template>
  <div class="hero-bg" aria-hidden="true">
    <div class="scanline"></div>
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

/* ── Background ─────────────────────────────────── */
.hero-bg {
  position: fixed;
  inset: 0;
  z-index: 0;
  background-image:
    linear-gradient(rgba(0, 189, 126, 0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0, 189, 126, 0.04) 1px, transparent 1px);
  background-size: 48px 48px;
  pointer-events: none;
}

.scanline {
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0px,
    transparent 3px,
    rgba(0, 0, 0, 0.08) 3px,
    rgba(0, 0, 0, 0.08) 4px
  );
  animation: scanmove 8s linear infinite;
}

@keyframes scanmove {
  0%   { background-position: 0 0; }
  100% { background-position: 0 100px; }
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
}

.radar-sweep {
  position: absolute;
  inset: 0;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: conic-gradient(
    from 0deg,
    transparent 0deg,
    rgba(0, 189, 126, 0.35) 40deg,
    transparent 60deg
  );
  animation: radar 3s linear infinite;
}

@keyframes radar {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

.hex-frame::after {
  content: "";
  position: absolute;
  inset: -3px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: linear-gradient(135deg, var(--color-accent), transparent 60%, var(--color-accent));
  z-index: -1;
  opacity: 0.7;
}

.online-badge {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  color: var(--color-accent);
  border: 1px solid rgba(0, 189, 126, 0.25);
  padding: 0.2rem 0.65rem;
  clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
  background: rgba(0, 189, 126, 0.06);
}

.pulse-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--color-accent);
  animation: blink 1.4s ease-in-out infinite;
  flex-shrink: 0;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.2; }
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
  background: linear-gradient(transparent, var(--color-accent), transparent);
}

.side-animation:hover::after {
  top: 25%;
  opacity: 1;
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
  color: rgba(235, 235, 235, 0.45);
}

.quotes .attr {
  color: rgba(0, 189, 126, 0.6);
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
}

.rownowaga {
  background-image: url("./assets/rownowaga.png");
  width: 257px;
  height: 256px;
  z-index: 2;
  position: relative;
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
