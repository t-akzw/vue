<template>
  <div class="input">
    <h1>{{ msg }}</h1>

    <EditCategory @reload_categories="reloadCategory($event)" />

    <div>
      <dx-chart ref="chart"
        :data-source="dataSource"
        title="JPY"
      >
        <dx-legend :visible="false"/>
        <dx-adaptive-layout :width="450"/>
        <dx-size :height="200"/>
        <dx-common-series-settings
          type="bar"
          argument-field="Date"
        />
        <dx-series
          value-field="JPY"
          name="JPY"
        />
      </dx-chart>
      <dx-data-grid
        id="clientGrid"
        :data-source="dataSource"
        :show-borders="true"
        :column-auto-width="true"
        :on-row-updated="saveGrid"
        :on-row-removed="saveGrid"
        :on-row-inserted="saveGrid"
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
          :width="125"
          data-field="Name"
          data-type="string"
        >
          <dx-required-rule/>
          <dx-lookup
            :data-source="categories"
            value-expr="Name"
            display-expr="Name"
          />
        </dx-column>
        <dx-column
          data-field="JPY"
          caption="JPY"
          data-type="number"
        >
          <dx-required-rule/>
        </dx-column>
        <dx-column
          data-field="Date"
          data-type="date"
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
  DxLookup,
} from 'devextreme-vue/data-grid';

import {
  DxChart,
  DxAdaptiveLayout,
  DxCommonSeriesSettings,
  DxSize,
  DxLegend,
  DxSeries,
} from 'devextreme-vue/chart';

import { datasources } from './data.js';

// https://js.devexpress.com/Documentation/Guide/Themes/Predefined_Themes/#Themes_in_Sites
import 'devextreme/dist/css/dx.common.css';
import 'devextreme/dist/css/dx.light.compact.css';

import EditCategory from './Input/EditCategory.vue'


export default {
  name: 'Hello',
  components: {
    DxDataGrid,
    DxColumn,
    DxPaging,
    DxPager,
    DxEditing,
    DxRequiredRule,
    DxLookup,
    DxChart,
    DxAdaptiveLayout,
    DxCommonSeriesSettings,
    DxSize,
    DxLegend,
    DxSeries,
    EditCategory,
  },
  props: {
    msg: String
  },
  data: function(){
    return {
      dataSource: datasources,
      pageSizes: [5, 10, 15, 50],
      categories: [],
    }
  },
  mounted() {
    if (localStorage.getItem('datasources')) {
      try {
        this.dataSource = JSON.parse(localStorage.getItem('datasources'));
      } catch(e) {
        localStorage.removeItem('datasources');
      }
    }
  },
  methods: {
    saveGrid() {
      localStorage.setItem('datasources', JSON.stringify(this.dataSource));
    },
    reloadCategory(eventArgs) {
      this.categories = eventArgs.cat
      this.dataSource = JSON.parse(localStorage.getItem('datasources'));
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
