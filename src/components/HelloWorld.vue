<script setup>
import { reactive, onMounted, watch } from 'vue'
import { TextScramble } from '../components/scramble'

const props = defineProps({
  msg: {
    type: String,
    required: true
  },
  cardEl: {
    type: Object,
    default: null
  }
})

const data = reactive({
  time: '0'
})

const calculateLightDistance = () => {
  const lightSpeed = 299792458
  const startTime = new Date("1989-01-06")
  const elapsedSeconds = (Date.now() - startTime) / 1000
  const distanceKm = (lightSpeed * elapsedSeconds) / 1000
  data.time = distanceKm.toFixed(0)
}

const setupMouseTracking = (card) => {
  card.addEventListener('mousemove', (event) => {
    const rect = card.getBoundingClientRect()
    const mouseY = event.clientY - rect.top
    card.style.setProperty('--slide-top', `${(mouseY / rect.height) * 100}%`)
    card.style.setProperty('--slide-opacity', 1)
  })

  card.addEventListener('mouseout', () => {
    card.style.setProperty('--slide-opacity', 0)
  })

  window.addEventListener('scroll', () => {
    const rect = card.getBoundingClientRect()
    const isInViewport = rect.top >= 0 && rect.bottom <= window.innerHeight
    if (isInViewport) {
      const glowTop = (window.scrollY - rect.top) / rect.height * 100
      card.style.setProperty('--slide-top', `${glowTop}%`)
      card.style.setProperty('--slide-opacity', 1)
    }
  })
}

const initScramble = () => {
  const phrases = [
    "This task was appointed to you.",
    "And if you do not find a way, no one will.",
    "Your time will come.",
    "You will face the same Evil",
    "and You will defeat it!",
    "&nbsp;",
    "Neo,",
    "sooner or later",
    "you're going to realize",
    "just as I did",
    "that there's a difference",
    "between knowing the path",
    "and walking the path",
    "&nbsp;",
    "The devil doesn't come dressed",
    "in a red cape and pointy horns.",
    "He comes as everything",
    "you've ever wished for...",
    "&nbsp;"
  ]

  const el = document.querySelector(".xtext")
  const fx = new TextScramble(el)

  let counter = 0
  const next = () => {
    fx.setText(phrases[counter]).then(() => {
      setTimeout(next, 2000)
    })
    counter = (counter + 1) % phrases.length
  }

  next()
}

onMounted(() => {
  setInterval(calculateLightDistance, 1000)
  initScramble()
})

watch(() => props.cardEl, (card) => {
  if (card) setupMouseTracking(card)
}, { immediate: true })
</script>

<template>
  <div class="greetings">
    <div class="name-block">
      <div class="prompt-prefix">&gt;_</div>
      <h1 class="glitch-name" :data-text="msg">{{ msg }}</h1>
    </div>

    <p class="role"><span class="bracket">[</span>IT Security Expert<span class="bracket">]</span></p>

    <div class="distance-stat">
      <span class="stat-label">LIGHT TRAVELED SINCE BIRTH</span>
      <span class="stat-value green">{{ data.time }} <span class="stat-unit">km</span></span>
    </div>

    <div class="divider"></div>

    <section>
      <h3><span class="idx">01</span> Projects</h3>
      <p>
        <a href="https://vulnrepo.com/home" target="_blank" rel="noopener">VULNREPO</a>,
        <a href="https://cifrex.org/" target="_blank" rel="noopener">cIFrex</a>,
        <a href="https://devilteam.pl/" target="_blank" rel="noopener">DEVIL TEAM</a>
        and many
        <a href="https://github.com/kac89?tab=repositories" target="_blank" rel="noopener">other projects</a>.
      </p>
    </section>

    <section>
      <h3><span class="idx">02</span> Research</h3>
      <p>
        <a href="https://www.exploit-db.com/?author=601" target="_blank" rel="noopener">Exploit Database</a>,
        <a href="http://0day.today/author/165" target="_blank" rel="noopener">My milw0rm</a>
      </p>
    </section>

    <section>
      <h3><span class="idx">03</span> Top Security Researchers</h3>
      <p>
        <a href="https://dbugs.ptsecurity.com/researchers/Kacper" target="_blank" rel="noopener">Kacper</a>
      </p>
    </section>

    <div class="divider"></div>

    <section class="contact-section">
      <h3><span class="idx">04</span> Contact</h3>
      <div class="contact-links">
        <a href="https://x.com/kacperybczynski" target="_blank" rel="noopener" class="contact-btn">
          <img src="../assets/x-social-media-white-round-icon.svg" width="20" height="20" alt="X (Twitter)" />
          <span>X / Twitter</span>
        </a>
        <a href="https://www.linkedin.com/in/kacperrybczynski/" target="_blank" rel="noopener" class="contact-btn">
          <img src="../assets/LinkedIN_white.svg" width="20" height="20" alt="LinkedIn" />
          <span>LinkedIn</span>
        </a>
      </div>
    </section>
  </div>
</template>

<style scoped>
/* ── Name block ─────────────────────────────────── */
.name-block {
  display: flex;
  align-items: baseline;
  gap: 0.6rem;
  flex-wrap: wrap;
}

.prompt-prefix {
  color: var(--color-accent);
  font-size: 1.4rem;
  font-weight: 100;
  flex-shrink: 0;
  text-shadow: 0 0 12px rgba(155, 0, 0, 0.7);
  animation: cursor-blink 1.2s step-end infinite;
}

@keyframes cursor-blink {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0; }
}

.glitch-name {
  font-weight: 500;
  font-size: 2.4rem;
  line-height: 1.1;
  color: var(--color-heading);
  position: relative;
  letter-spacing: 0.02em;
}

.glitch-name::before,
.glitch-name::after {
  content: attr(data-text);
  position: absolute;
  inset: 0;
  color: var(--color-heading);
}

/* Fire orange channel */
.glitch-name::before {
  animation: glitch-top 6s infinite linear;
  clip-path: inset(0 0 70% 0);
  color: #FF5500;
  opacity: 0;
}

/* Blood red channel */
.glitch-name::after {
  animation: glitch-bot 6s infinite linear;
  clip-path: inset(70% 0 0 0);
  color: #8B0000;
  opacity: 0;
}

@keyframes glitch-top {
  0%,  94%  { opacity: 0; transform: translate(0, 0); }
  94.5%     { opacity: 1; transform: translate(-3px, -2px); }
  95%        { opacity: 1; transform: translate( 3px,  1px); }
  96%        { opacity: 0; transform: translate(0, 0); }
  98%        { opacity: 1; transform: translate(-2px, 0);    }
  98.5%      { opacity: 0; transform: translate(0, 0); }
  100%       { opacity: 0; }
}

@keyframes glitch-bot {
  0%,  95%  { opacity: 0; transform: translate(0, 0); }
  95.5%     { opacity: 1; transform: translate( 4px,  2px); }
  96.5%     { opacity: 1; transform: translate(-2px, -1px); }
  97%        { opacity: 0; transform: translate(0, 0); }
  100%       { opacity: 0; }
}

/* ── Role ───────────────────────────────────────── */
.role {
  font-size: 0.85rem;
  letter-spacing: 0.18em;
  color: rgba(200, 168, 112, 0.55);
  text-transform: uppercase;
}

.bracket {
  color: var(--color-gold);
  opacity: 0.7;
}

/* ── Distance stat ──────────────────────────────── */
.distance-stat {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
  border-left: 2px solid var(--color-accent);
  padding-left: 0.85rem;
  margin: 0.25rem 0;
  box-shadow: -3px 0 12px rgba(155, 0, 0, 0.25);
}

.stat-label {
  font-size: 0.62rem;
  letter-spacing: 0.14em;
  color: rgba(200, 168, 112, 0.4);
  text-transform: uppercase;
}

.stat-value {
  font-size: 1.5rem;
  letter-spacing: 0.04em;
  line-height: 1;
  color: var(--color-gold);
  text-shadow: 0 0 14px rgba(200, 150, 12, 0.4);
}

.stat-unit {
  font-size: 0.75rem;
  opacity: 0.7;
}

/* ── Divider ────────────────────────────────────── */
.divider {
  height: 1px;
  background: linear-gradient(90deg, var(--color-accent), transparent);
  opacity: 0.3;
  margin: 0.25rem 0;
  box-shadow: 0 0 8px rgba(155, 0, 0, 0.3);
}

/* ── Sections ───────────────────────────────────── */
.greetings {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

section {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
}

h3 {
  font-size: 0.72rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: rgba(200, 168, 112, 0.4);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.idx {
  color: var(--color-gold);
  font-size: 0.62rem;
  opacity: 0.75;
  font-variant-numeric: tabular-nums;
  text-shadow: 0 0 8px rgba(200, 150, 12, 0.4);
}

/* ── Contact ────────────────────────────────────── */
.contact-links {
  display: flex;
  gap: 0.6rem;
  flex-wrap: wrap;
}

.contact-btn {
  display: flex;
  align-items: center;
  gap: 0.45rem;
  font-size: 0.78rem;
  letter-spacing: 0.06em;
  padding: 0.35rem 0.75rem;
  border: 1px solid rgba(155, 0, 0, 0.35);
  clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  background: rgba(155, 0, 0, 0.06);
  color: rgba(200, 168, 112, 0.75);
  transition: background 0.3s, border-color 0.3s, box-shadow 0.3s;
}

.contact-btn:hover {
  background: rgba(155, 0, 0, 0.18) !important;
  border-color: rgba(155, 0, 0, 0.65);
  box-shadow: 0 0 16px rgba(155, 0, 0, 0.25), inset 0 0 8px rgba(155, 0, 0, 0.1);
  color: var(--color-heading);
}

/* ── Alignment: mobile center, desktop left ─────── */
.greetings h1,
.greetings p,
.greetings h3 {
  text-align: center;
}

.name-block {
  justify-content: center;
}

.distance-stat {
  align-items: center;
  border-left: none;
  padding-left: 0;
  border-top: 2px solid var(--color-accent);
  padding-top: 0.5rem;
  box-shadow: 0 -3px 12px rgba(155, 0, 0, 0.2);
}

.contact-links {
  justify-content: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings p,
  .greetings h3 {
    text-align: left;
  }

  .name-block {
    justify-content: flex-start;
  }

  .distance-stat {
    align-items: flex-start;
    border-top: none;
    padding-top: 0;
    border-left: 2px solid var(--color-accent);
    padding-left: 0.85rem;
    box-shadow: -3px 0 12px rgba(155, 0, 0, 0.25);
  }

  .contact-links {
    justify-content: flex-start;
  }
}
</style>
