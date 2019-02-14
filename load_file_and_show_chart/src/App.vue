<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <FileLoad msg='FileLoad!!' />
    <ShowFigures />
  </div>
</template>

<script>
import FileLoad from './components/FileLoad.vue'

export default {
  name: 'app',
  components: {
    FileLoad
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>