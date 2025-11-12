<script setup>
import { reactive, onMounted } from 'vue'
import {TextScramble} from '../components/scramble';

defineProps({
  msg: {
    type: String,
    required: true
  }
});

const data = reactive({
    time: '0'
});

const getTravelofMyLife = () => {

  const card = document.querySelector('header .side-animation');
  const afterElement = window.getComputedStyle(card, 'after');

  card.addEventListener('mousemove', (event) => {
      const cardRect = card.getBoundingClientRect();
      const mouseY = event.clientY - cardRect.top; // Get relative Y position of mouse within card

      const top = `${mouseY / cardRect.height * 100}%`; // Update top position based on mouse Y
      card.style.setProperty('--slide-top', top);
      card.style.setProperty('--slide-opacity', 1);
  });

  window.addEventListener('scroll', () => {
      const cardRect = card.getBoundingClientRect();
      isCardInViewport = cardRect.top >= 0 && cardRect.bottom <= window.innerHeight;

      if (isCardInViewport) {
          const scrollY = window.scrollY; // Get current scroll position
          const cardHeight = cardRect.height;
          const cardTop = cardRect.top;

          const glowTop = (scrollY - cardTop) / cardHeight * 100; // Calculate glow position based on scrollY

          const top = `${glowTop}%`;
          card.style.setProperty('--slide-top', top);
          card.style.setProperty('--slide-opacity', 1);
      }
  });
  card.addEventListener('mouseout', () => {
      card.style.setProperty('--slide-opacity', 0);
  });

  const lightSpeed = 299792458; // prędkość światła w próżni w metrach na sekundę
  const startTime = new Date("1989-01-06"); // czas początkowy w milisekundach       
  const secondsInYear = 365.25 * 24 * 60 * 60; // liczba sekund w roku (uwzględniając rok przestępny)

  let distanceMeters = 0;
  // funkcja aktualizująca dystans na podstawie upływającego czasu

  const currentTime = Date.now(); // aktualny czas w milisekundach
  const elapsedTimeSeconds = (currentTime - startTime) / 1000; // upłynięty czas w sekundach
  distanceMeters = lightSpeed * elapsedTimeSeconds;


  // obliczamy dystans w kilometrach
  const distanceKilometers = distanceMeters / 1000;
  const yearsp = elapsedTimeSeconds / 31536000;

  // wyświetlamy wynik w konsoli
  //console.log(`Dystans pokonany przez foton w ciągu ${yearsp.toFixed(2)} lat to ${distanceKilometers.toFixed(2)} kilometrów.`);
  //data.time = yearsp.toFixed(2) + ":" + distanceKilometers.toFixed(2);

  data.time = distanceKilometers.toFixed(0);
}

onMounted(() => {
    setInterval(getTravelofMyLife, 1000);

  // ——————————————————————————————————————————————————
  // Settings cypher
  // ——————————————————————————————————————————————————
  
  const phrases = [
    "This task was appointed to you.", //lotr
    "And if you do not find a way, no one will.",
    "Your time will come.",
    "You will face the same Evil",
    "and You will defeat it!",
    "&nbsp;",
    "Neo,", //matrix
    "sooner or later",
    "you're going to realize",
    "just as I did",
    "that there's a difference",
    "between knowing the path",
    "and walking the path",
    "&nbsp;",
    "The devil doesn't come dressed",//Tucker Max
    "in a red cape and pointy horns.",
    "He comes as everything",
    "you've ever wished for...",
    "&nbsp;"
  ];
  
  const el = document.querySelector(".xtext");
  const fx = new TextScramble(el);
  
  let counter = 0;
  const next = () => {
    fx.setText(phrases[counter]).then(() => {
      setTimeout(next, 2000);
    });
    counter = (counter + 1) % phrases.length;
  };
  
  next();

  });
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <p>IT Security Expert</p><br>
    <h3>
      My projects<br>
      <a href="https://vulnrepo.com/home" target="_blank" rel="noopener">VULNREPO</a>, 
      <a href="https://cifrex.org/" target="_blank" rel="noopener">cIFrex</a>, 
      <a href="https://devilteam.pl/" target="_blank" rel="noopener">DEVIL TEAM</a><br> and many 
      <a href="https://github.com/kac89?tab=repositories" target="_blank" rel="noopener">other projects</a>.

    </h3><br>
    <h3>
      Research<br>
      <a href="https://www.exploit-db.com/?author=601" target="_blank" rel="noopener">Exploit Database</a>, 
      <a href="http://0day.today/author/165" target="_blank" rel="noopener">My milw0rm</a>

    </h3><br>

        <h3>
      Top Security Researchers<br>
      <a href="https://dbugs.ptsecurity.com/researchers/Kacper" target="_blank" rel="noopener">Kacper</a>

    </h3><br>

    <h3>My journey</h3>
    <p class="green"><h3>{{ data.time }}</h3></p><br>
    <h3>
      Contact<br>
      <a href="https://x.com/kacperybczynski" target="_blank" rel="noopener"><img src="../assets/x-social-media-white-round-icon.svg" width="32" height="32" /></a>
      <a href="https://www.linkedin.com/in/kacperrybczynski/" target="_blank" rel="noopener"><img src="../assets/LinkedIN_white.svg" width="32" height="32" /></a>
    </h3>
  </div>
  <br><br>
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

.greetings h1,
.greetings p,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings p,
  .greetings h3 {
    text-align: left;
  }
}
</style>
