<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Recaptcha msg="Testando CAPTCHA"/>
  </div>
</template>

<script>
// import Hcaptcha from './components/Hcaptcha.vue'
import Recaptcha from './components/Recaptcha.vue'

export default {
  name: 'App',
  components: {
    // Hcaptcha,
    Recaptcha
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
