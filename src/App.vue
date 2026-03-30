<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const sideAnimationEl = ref(null)
</script>

<template>
  <header>
    <div class="avatar-wrapper">
      <div class="card growborder">
        <div class="inner">
          <img alt="Kacper" class="logo" src="./assets/kacper.jpg" width="155" height="155" />
        </div>
      </div>
    </div>

    <div class="wrapper side-animation" ref="sideAnimationEl">
      <HelloWorld msg="Kacper Rybczyński" :card-el="sideAnimationEl" />
    </div>
  </header>

  <main>
    <section class="quotes">
      <p>"First rule of business, protect your investment."</p>
      <p>— Etiquette of the Banker, 1775</p>

      <p>"The only way to get smarter is by playing a smarter opponent."</p>
      <p>— Fundamentals of Chess, 1883</p>
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

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0;
}

.avatar-wrapper {
  display: grid;
  place-items: center;
}

.quotes {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  margin-bottom: 2rem;
}

.quotes p + p:is(:nth-child(2), :nth-child(4)) {
  margin-bottom: 1rem;
}

.symbol-wrapper {
  display: grid;
  place-items: center;
  margin-bottom: 1rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.side-animation {
  transition: transform 0.18s;
  position: relative;
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
  to {
    transform: rotate(-360deg);
  }
}

header .growborder {
  margin: 20px;
  width: 160px;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

header .growborder .inner {
  position: relative;
  z-index: 1;
  margin: 2px;
}

header .growborder::before {
  content: "";
  display: block;
  background: linear-gradient(
    90deg,
    rgba(255, 255, 255, 0) 0%,
    var(--color-accent) 50%,
    rgba(255, 255, 255, 0) 100%
  );
  height: 300px;
  width: 150px;
  position: absolute;
  animation: rotate 5s linear infinite;
  z-index: 0;
  top: 50%;
  transform-origin: top center;
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
</style>
