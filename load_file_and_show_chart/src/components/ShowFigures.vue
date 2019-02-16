<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  props: {
    chartdata: {
      type: Array,
    },
  },
  mounted() {
    this.renderChart({
      labels: ['1', '2', '3', '4', '5', '6', '7'],
      datasets: [
        {
          label: 'Chart',
          backgroundColor: '#2c3e50',
          data: this.chartdata
        }
      ]
    }, {responsive: true, maintainAspectRatio: false})
  },
}
</script>

<style>
  .small {
    max-width: 600px;
    margin:  150px auto;
  }
</style>