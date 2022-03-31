<template>
  <div id="app">
    <BotMain />
  </div>
</template>

<script>
import BotMain from './components/BotMain.vue'
export default {
  name: 'App',
  components: {
    BotMain
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
