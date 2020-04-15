<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>COVID - 19</h1>  
    <p>Pagina web desarrollada para conocer las estadisticas del covid-19 alrededor del mundo </p>  
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
