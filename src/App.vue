<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { reactive, onMounted } from 'vue'

const data = reactive({
    time: ''
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
  <header>
    <img alt="Kacper" class="logo" src="./assets/kacper.jpg" width="155" height="155" />

    <div class="wrapper">
      <HelloWorld msg="Kacper Rybczyński" />
    </div>
  </header>

  <main>
    <div>
        <p>"First rule of business, protect your investment."</p>
        <p>— Etiquette of the Banker, 1775</p>
        <br>
        <p>"The only way to get smarter is by playing a smarter opponent."</p>
        <p>— Fundamentals of Chess, 1883</p>
        <br>
        <div style="display:grid; place-items: center;">
          <img alt="Balance" class="logo" src="./assets/balance.png" width="350" />
          <br>
        </div>
        <br>
        <div style="display:grid; place-items: center;padding-right: 25px;">
          <h2 class="green" v-html="data.time"></h2>
        </div>
        
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    /*padding-right: calc(var(--section-gap) / 2);*/
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
