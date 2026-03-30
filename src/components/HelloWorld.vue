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
    <h1 class="green">{{ msg }}</h1>
    <p>IT Security Expert</p>

    <section>
      <h3>My projects</h3>
      <p>
        <a href="https://vulnrepo.com/home" target="_blank" rel="noopener">VULNREPO</a>,
        <a href="https://cifrex.org/" target="_blank" rel="noopener">cIFrex</a>,
        <a href="https://devilteam.pl/" target="_blank" rel="noopener">DEVIL TEAM</a>
        and many
        <a href="https://github.com/kac89?tab=repositories" target="_blank" rel="noopener">other projects</a>.
      </p>
    </section>

    <section>
      <h3>Research</h3>
      <p>
        <a href="https://www.exploit-db.com/?author=601" target="_blank" rel="noopener">Exploit Database</a>,
        <a href="http://0day.today/author/165" target="_blank" rel="noopener">My milw0rm</a>
      </p>
    </section>

    <section>
      <h3>Top Security Researchers</h3>
      <p>
        <a href="https://dbugs.ptsecurity.com/researchers/Kacper" target="_blank" rel="noopener">Kacper</a>
      </p>
    </section>

    <section>
      <h3>My journey</h3>
      <h3 class="green">{{ data.time }}</h3>
    </section>

    <section>
      <h3>Contact</h3>
      <div class="contact-links">
        <a href="https://x.com/kacperybczynski" target="_blank" rel="noopener">
          <img src="../assets/x-social-media-white-round-icon.svg" width="32" height="32" alt="X (Twitter)" />
        </a>
        <a href="https://www.linkedin.com/in/kacperrybczynski/" target="_blank" rel="noopener">
          <img src="../assets/LinkedIN_white.svg" width="32" height="32" alt="LinkedIn" />
        </a>
      </div>
    </section>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.greetings h1,
.greetings p,
.greetings h3 {
  text-align: center;
}

section {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.contact-links {
  display: flex;
  gap: 0.5rem;
  justify-content: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings p,
  .greetings h3 {
    text-align: left;
  }

  .contact-links {
    justify-content: flex-start;
  }
}
</style>
