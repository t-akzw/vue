<template>
  <div class="input">
    <h1>{{ msg }}</h1>
    <div class="addcategory">
      <!-- Ver.01: 履歴の削除機能を実装するまでこちらに削除機能を入れておく -->
      <div v-for="(cat, n) in cats">
        <p>
          <span class="cat">{{ cat }}</span>
          <button @click="removeCategory(n)">Remove</button>
        </p>
      </div>

      <input type="text" v-model="newCat">
      <button @click="addCategory">Add</button>

      <select v-model="selected">
        <option v-for="cat in cats" v-bind:value="cat">
          {{ cat }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    msg: String
  },
  data: function(){
    return {
      cats: [],
      newCat: null,
      selected: null,
    }
  },
  mounted() {
    if (localStorage.getItem('cats')) {
      try {
        this.cats = JSON.parse(localStorage.getItem('cats'));
        if (!this.cats[0]) {
          // Ver.01: 後々は設定で持たせる+初回ログイン後に一回だけ呼び出すようにする。
          this.cats = [ '食費', '光熱費', '家賃', '交際費', '医療費', '日用品', '交通費', '給与' ];
          this.saveCategory();
        }
      } catch(e) {
        localStorage.removeItem('cats');
      }
    }
  },
  methods: {
    addCategory() {
      if (!this.newCat) {
        return;
      }
      this.cats.push(this.newCat);
      this.newCat = '';
      this.saveCategory();
    },
    removeCategory(x) {
      this.cats.splice(x, 1);
      this.saveCategory();
    },
    saveCategory() {
      const parsed = this.parseCategory();
      localStorage.setItem('cats', parsed);
    },
    parseCategory() {
      let removed_duplicated = Array.from(new Set(this.cats));
      this.cats = removed_duplicated;
      return JSON.stringify(this.cats);
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
