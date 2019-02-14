<template>
  <div id="post">
    <input type="file" v-on:change="onFileLoad" accept="text/*,.csv">
    <p>{{ fileinfo }}</p>
    <textarea v-if="txt !== ''">{{ txt }}</textarea>
  </div>
</template>

<script>
export default {
  props: {
    msg: String
  },
  data: function(){
    return {
      fileinfo: '',
      txt: ''
    }
  },
  methods: {
    onFileLoad: function(e) {
      const file = e.target.files[0]
      if (!file) { return false }
      this.fileinfo = `${this.msg} [${file.name} | ${file.size} | ${file.type} ]`

      const tmp = this
      const reader = new FileReader()
      reader.onload = function(e){
        tmp.txt = e.target.result
      }
      reader.readAsText(file)
    },
    props: {
      msg: String
    }
  }
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