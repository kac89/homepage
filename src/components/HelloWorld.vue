<script setup>
import { reactive, onMounted } from 'vue'

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
  });
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <p>IT Security Expert</p><br>
    <h3>
      My projects<br>
      <a href="https://vulnrepo.com/home" target="_blank" rel="noopener">VULNRΞPO</a>, 
      <a href="https://cifrex.org/" target="_blank" rel="noopener">cIFrex</a>, 
      <a href="https://devilteam.pl/" target="_blank" rel="noopener">DEVIL TEAM</a><br> and many 
      <a href="https://github.com/kac89?tab=repositories" target="_blank" rel="noopener">others</a>.

    </h3><br>
    <h3>
      Research<br>
      <a href="https://www.exploit-db.com/?author=601" target="_blank" rel="noopener">Exploit Database</a>, 
      <a href="http://0day.today/author/165" target="_blank" rel="noopener">My milw0rm</a>

    </h3><br>
    <h3>My journey</h3>
    <p class="green"><h3>{{ data.time }}</h3></p><br>
    <h3>
      Contact<br>
      <a href="https://twitter.com/kacperybczynski" target="_blank" rel="noopener">@kacperybczynski</a><br>
      <a href="https://github.com/kac89" target="_blank" rel="noopener">@kac89</a>
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
