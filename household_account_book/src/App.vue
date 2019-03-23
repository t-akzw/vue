<template>
  <div id="app">
    <Input msg="Household account book(Ver.01)"/>
  </div>
</template>

<script>
import Input from './components/Input.vue'

export default {
  name: 'app',
  components: {
    Input
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
