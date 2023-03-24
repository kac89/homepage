<script setup>
import HelloWorld from './components/HelloWorld.vue'
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
