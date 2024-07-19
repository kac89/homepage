<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>

    <div style="display:grid; place-items: center;">
      <div class="card growborder">
        <div class="inner">
          <img alt="Kacper" class="logo" src="./assets/kacper.jpg" width="155" height="155" />
        </div>
      </div>
    </div>



    <div class="wrapper side-animation">
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

        <div class="output">
          <div class="smoki">
          </div>
          <div class="rownowaga">
          </div>
        </div>

        <br>
      </div>
      <br>
      <div class="cypher">
        <div class="xtext"></div>
      </div>
      <br>


    </div>
  </main>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    /*padding-right: calc(var(--section-gap) / 2);*/
  }

  .logo {
    display: block;
    margin: 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}


.side-animation {
  transition: transform .180s;
  position: relative
}

.side-animation:after {
  content: "";
  height: 160px;
  width: 2px;
  position: absolute;
  right: 0;
  top: 10%;
  transition: top, opacity;
  transition-duration: 0s, 0s;
  transition-timing-function: ease, ease;
  transition-duration: 400ms;
  transition-timing-function: ease;
  background: linear-gradient(transparent, hsla(160, 100%, 37%, 1), transparent);
  opacity: 1
}

.side-animation:after {
  top: 65%;
  opacity: 0
}

.side-animation:hover:after {
  top: 25%;
  opacity: 1
}


.smoki {
  background-image: url("./assets/smoki.png");
  width: 257px;
  height: 256px;
  -webkit-animation: spin 12s linear infinite;
  -moz-animation: spin 12s linear infinite;
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

@-moz-keyframes spin {
  100% {
    -moz-transform: rotate(-360deg);
  }
}

@-webkit-keyframes spin {
  100% {
    -webkit-transform: rotate(-360deg);
  }
}

@keyframes spin {
  100% {
    -webkit-transform: rotate(-360deg);
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
  background: linear-gradient(90deg,
      rgba(255, 255, 255, 0) 0%,
      hsla(160, 100%, 37%, 1) 50%,
      rgba(255, 255, 255, 0) 100%);
  height: 300px;
  width: 150px;
  transform: translate(0);
  position: absolute;
  animation: rotate 5s linear forwards infinite;
  z-index: 0;
  top: 50%;
  transform-origin: top center;
}

@keyframes rotate {
  from {
    transform: rotate(0);
  }

  to {
    transform: rotate(360deg);
  }
}

</style>
