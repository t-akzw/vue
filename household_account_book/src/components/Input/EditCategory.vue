<template>
  <div class="edit_category">
    <toggle-button
      @change="onChangeEditCategory"
      :value="false"
      :labels="{checked: 'Editing', unchecked: 'Edit Category'}"
      color="#82C7EB"
      :sync="true"
      :width=100
    />
    <div v-if="isEditCategory">
      <dx-data-grid
        :data-source="categories"
        :show-borders="true"
        :column-auto-width="true"
        :on-row-updated="saveCategory"
        :on-row-removed="saveCategory"
        :on-row-inserted="saveCategory"
      >
        <dx-editing
          :allow-updating="true"
          :allow-deleting="true"
          :allow-adding="true"
          mode="batch"
        />
        <dx-paging :enabled="true" :page-size="5"/>
        <dx-pager
          :show-page-size-selector="true"
          :allowed-page-sizes="pageSizes"
          :show-info="true"
        />

        <dx-column
          data-field="Name"
        >
          <dx-required-rule/>
        </dx-column>
      </dx-data-grid>
    </div>

  </div>
</template>

<script>

import {
  DxDataGrid,
  DxColumn,
  DxPaging,
  DxPager,
  DxEditing,
  DxRequiredRule,
} from 'devextreme-vue/data-grid';
import { ToggleButton } from 'vue-js-toggle-button';

import { cat_data } from '../data.js';

export default {
  name: 'Hello',
  components: {
    ToggleButton,
    DxDataGrid,
    DxColumn,
    DxPaging,
    DxPager,
    DxEditing,
    DxRequiredRule,
  },
  props: {
    msg: String,
  },
  data: function(){
    return {
      isEditCategory: false,
      categories: null,
      pageSizes: [5, 10, 15, 50],
    }
  },
  mounted() {
    try {
      this.loadCategory()
    } catch(e) {
      localStorage.removeItem('categories');
    }
  },
  methods: {
    loadCategory() {
      const cat = localStorage.getItem('categories')
      if (cat === undefined || cat === null) {
        this.categories = cat_data
      } else {
        this.categories = JSON.parse(cat)
      }
      this.saveCategory()
    },
    onChangeEditCategory() {
      this.isEditCategory = !this.isEditCategory
    },
    saveCategory() {
      const parsed = this.parseCategory();
      localStorage.setItem('categories', parsed);
      this.$emit('reload_categories', {
        cat: this.categories,
      })
    },
    parseCategory() {
      return JSON.stringify(this.categories);
    },
  }
}
</script>

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
