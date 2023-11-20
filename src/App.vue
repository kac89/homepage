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

          <div class="output">
            <div class="smoki">
            </div>
            <div class="rownowaga">
            </div>
          </div>

          <br>
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



.smoki {
			background-image: url("smoki.png");
			width: 257px;
			height: 256px;
			-webkit-animation:spin 12s linear infinite;
		  -moz-animation:spin 12s linear infinite;
		  animation:spin 12s linear infinite;
		  z-index: 1;
		  position: absolute;
		}
		.rownowaga {
			background-image: url("rownowaga.png");
			width: 257px;
			height: 256px;
			z-index: 2;
      position: relative;
		}

		.output {
			width: 257px;
			height: 256px;
		}

		@-moz-keyframes spin { 
		    100% { -moz-transform: rotate(-360deg); } 
		}
		@-webkit-keyframes spin { 
		    100% { -webkit-transform: rotate(-360deg); } 
		}
		@keyframes spin { 
		    100% { 
		        -webkit-transform: rotate(-360deg); 
		        transform:rotate(-360deg); 
		    } 
		}
</style>
