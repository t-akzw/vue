<template>
  <div id="post">
    <input type="file" v-on:change="onFileLoad" accept="text/*,.csv">
    <p>FileLoad {{ text }}</p>
  </div>
</template>

<script>

export default {
  data: function(){
    return {
      text: ''
    }
  },
  methods: {
    onFileLoad: function(e) {
      const file = e.target.files[0]
      if (!file) { return false }

      const tmp = this
      const reader = new FileReader()
      reader.onload = function(e){
        tmp.text = e.target.result.replace(/\r?\n/g, '').split(',').map( str => parseInt(str, 10) )
      }
      reader.readAsText(file)
    },
  },
  updated: function() {
    this.$emit('input', {
      text: this.text,
    })
  },
  mounted: function() {
    this.text = this.value.text
  },
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>