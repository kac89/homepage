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
    "&nbsp;",
    "You are the Shifter.",
    "You alone can move between the worlds.",
    "&nbsp;",
    "The Balance must be maintained.",
    "&nbsp;",
    "Every story has a beginning,",
    "a middle, and an end.",
    "Not necessarily in that order.",
    "&nbsp;",
    "This journey has no end.",
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
      <span class="stat-label">✦ LIGHT TRAVELED SINCE BIRTH ✦</span>
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
  text-shadow:
    0 0 12px rgba(155, 0, 0, 0.8),
    0 0 28px rgba(155, 0, 0, 0.35);
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
  text-shadow: 0 0 30px rgba(200, 150, 12, 0.12);
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
  animation: glitch-top 5s infinite linear;
  clip-path: inset(0 0 70% 0);
  color: #FF5500;
  opacity: 0;
}

/* Blood red channel */
.glitch-name::after {
  animation: glitch-bot 5s infinite linear;
  clip-path: inset(70% 0 0 0);
  color: #8B0000;
  opacity: 0;
}

@keyframes glitch-top {
  0%,  92%  { opacity: 0; transform: translate(0, 0); }
  92.5%     { opacity: 1; transform: translate(-4px, -2px); }
  93%        { opacity: 1; transform: translate( 4px,  2px); }
  94%        { opacity: 0; transform: translate(0, 0); }
  96%        { opacity: 1; transform: translate(-3px, 0);    }
  96.8%      { opacity: 0; transform: translate(0, 0); }
  100%       { opacity: 0; }
}

@keyframes glitch-bot {
  0%,  93%  { opacity: 0; transform: translate(0, 0); }
  93.5%     { opacity: 1; transform: translate( 5px,  3px); }
  94.8%     { opacity: 1; transform: translate(-3px, -2px); }
  95.5%      { opacity: 0; transform: translate(0, 0); }
  100%       { opacity: 0; }
}

/* ── Role ───────────────────────────────────────── */
.role {
  font-size: 0.85rem;
  letter-spacing: 0.18em;
  color: rgba(200, 168, 112, 0.58);
  text-transform: uppercase;
}

.bracket {
  color: var(--color-gold);
  opacity: 0.75;
}

/* ── Distance stat ──────────────────────────────── */
.distance-stat {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
  border-left: 2px solid var(--color-accent);
  padding-left: 0.85rem;
  margin: 0.25rem 0;
  box-shadow: -3px 0 16px rgba(155, 0, 0, 0.3);
  background: linear-gradient(90deg, rgba(155, 0, 0, 0.06) 0%, transparent 100%);
  padding-top: 0.3rem;
  padding-bottom: 0.3rem;
}

.stat-label {
  font-size: 0.60rem;
  letter-spacing: 0.12em;
  color: rgba(200, 168, 112, 0.42);
  text-transform: uppercase;
}

.stat-value {
  font-size: 1.5rem;
  letter-spacing: 0.04em;
  line-height: 1;
  color: var(--color-gold);
  text-shadow:
    0 0 14px rgba(200, 150, 12, 0.5),
    0 0 30px rgba(200, 150, 12, 0.2);
}

.stat-unit {
  font-size: 0.75rem;
  opacity: 0.7;
}

/* ── Divider ────────────────────────────────────── */
.divider {
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(155, 0, 0, 0.55),
    rgba(200, 150, 12, 0.3),
    rgba(155, 0, 0, 0.55),
    transparent
  );
  opacity: 0.6;
  margin: 0.25rem 0;
  box-shadow: 0 0 8px rgba(155, 0, 0, 0.3);
}

.divider::before {
  content: "◆";
  position: absolute;
  top: -0.55rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 0.55rem;
  color: rgba(155, 0, 0, 0.65);
  background: var(--color-background);
  padding: 0 0.45rem;
  text-shadow: 0 0 10px rgba(155, 0, 0, 0.7);
}

/* ── Sections ───────────────────────────────────── */
.greetings {
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}

section:not(.contact-section) {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  border: 1px solid rgba(155, 0, 0, 0.2);
  background: linear-gradient(135deg, rgba(28, 0, 0, 0.38) 0%, rgba(8, 0, 0, 0.52) 100%);
  padding: 0.65rem 0.9rem;
  clip-path: polygon(0 0, calc(100% - 8px) 0, 100% 8px, 100% 100%, 8px 100%, 0 calc(100% - 8px));
  transition: border-color 0.35s, box-shadow 0.35s;
  overflow: hidden;
}

/* Shift ripple on hover — reality tearing between worlds */
section:not(.contact-section)::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 50%;
  background: radial-gradient(circle at 50% 50%, rgba(0, 180, 140, 0.18) 0%, transparent 65%);
  transform: scale(0);
  opacity: 0;
  transition: transform 0.55s ease-out, opacity 0.55s ease-out;
  pointer-events: none;
}

section:not(.contact-section):hover::before {
  transform: scale(2.8);
  opacity: 1;
}

/* ── World-tag accent — left edge glow per section ── */
/* Projects → D2 fire */
section:not(.contact-section):nth-of-type(1) {
  border-left-color: rgba(155, 0, 0, 0.55);
  box-shadow: -3px 0 0 rgba(155, 0, 0, 0.7), inset 0 0 0 transparent;
}
section:not(.contact-section):nth-of-type(1):hover {
  border-color: rgba(155, 0, 0, 0.48);
  box-shadow:
    -3px 0 0 rgba(200, 75, 0, 0.8),
    0 0 24px rgba(155, 0, 0, 0.14),
    inset 0 0 30px rgba(90, 0, 0, 0.08);
}

/* Research → TLJ Arcadia teal */
section:not(.contact-section):nth-of-type(2) {
  border-left-color: rgba(13, 74, 92, 0.55);
  box-shadow: -3px 0 0 rgba(13, 74, 92, 0.7), inset 0 0 0 transparent;
}
section:not(.contact-section):nth-of-type(2):hover {
  border-color: rgba(13, 74, 92, 0.48);
  box-shadow:
    -3px 0 0 rgba(0, 130, 100, 0.8),
    0 0 24px rgba(13, 74, 92, 0.14),
    inset 0 0 30px rgba(0, 50, 40, 0.08);
}

/* Top Researchers → D2 gold */
section:not(.contact-section):nth-of-type(3) {
  border-left-color: rgba(200, 150, 12, 0.45);
  box-shadow: -3px 0 0 rgba(200, 150, 12, 0.65), inset 0 0 0 transparent;
}
section:not(.contact-section):nth-of-type(3):hover {
  border-color: rgba(200, 150, 12, 0.42);
  box-shadow:
    -3px 0 0 rgba(200, 150, 12, 0.8),
    0 0 24px rgba(200, 150, 12, 0.12),
    inset 0 0 30px rgba(80, 50, 0, 0.08);
}

.contact-section {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
}

h3 {
  font-size: 0.72rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: rgba(200, 168, 112, 0.45);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding-bottom: 0.28rem;
  border-bottom: 1px solid rgba(155, 0, 0, 0.12);
  margin-bottom: 0.12rem;
}

.idx {
  color: var(--color-gold);
  font-size: 0.62rem;
  opacity: 0.78;
  font-variant-numeric: tabular-nums;
  text-shadow: 0 0 10px rgba(200, 150, 12, 0.5);
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
  padding: 0.4rem 0.85rem;
  border: 1px solid rgba(155, 0, 0, 0.38);
  clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  background: linear-gradient(135deg, rgba(155, 0, 0, 0.08) 0%, rgba(60, 0, 0, 0.12) 100%);
  color: rgba(200, 168, 112, 0.78);
  transition: background 0.3s, border-color 0.3s, box-shadow 0.3s, color 0.3s;
}

.contact-btn:hover {
  background: linear-gradient(135deg, rgba(155, 0, 0, 0.22) 0%, rgba(80, 0, 0, 0.28) 100%) !important;
  border-color: rgba(155, 0, 0, 0.7);
  box-shadow:
    0 0 20px rgba(155, 0, 0, 0.28),
    inset 0 0 12px rgba(155, 0, 0, 0.12);
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
  box-shadow: 0 -3px 16px rgba(155, 0, 0, 0.22);
  background: linear-gradient(180deg, rgba(155, 0, 0, 0.05) 0%, transparent 100%);
  padding-bottom: 0.3rem;
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
    box-shadow: -3px 0 16px rgba(155, 0, 0, 0.28);
    background: linear-gradient(90deg, rgba(155, 0, 0, 0.06) 0%, transparent 100%);
  }

  .contact-links {
    justify-content: flex-start;
  }
}
</style>
