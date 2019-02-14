<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  mounted() {
    this.renderChart({
      labels: ['1', '2', '3', '4', '5', '6', '7'],
      datasets: [
        {
          label: 'Chart',
          backgroundColor: '#2c3e50',
          data: [0, 30, 60, 0, 60, 30, 0]
        }
      ]
    }, {responsive: true, maintainAspectRatio: false})
  }
}
</script>

<style>
  .small {
    max-width: 600px;
    margin:  150px auto;
  }
</style>