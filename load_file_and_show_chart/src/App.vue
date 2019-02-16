<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <FileLoad v-model="loaddata" />
    <show-figures v-if="cdata.text !== ''" v-bind:chartdata="this.cdata.text" />
  </div>
</template>

<script>
import FileLoad from './components/FileLoad.vue'
import ShowFigures from './components/ShowFigures.vue'

export default {
  name: 'app',
  components: {
    FileLoad,
    ShowFigures
  },
  data: function(){
    return {
      loaddata: {
        text: ''
      },
      cdata: {
        text: ''
      }
    }
  },
  watch: {
    loaddata: function() {
      this.cdata.text = this.loaddata.text
    }
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