<script setup>

defineProps({
  msg: {
    type: String,
    required: true
  }
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
