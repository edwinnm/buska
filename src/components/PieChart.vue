<script>
  import { Pie } from 'vue-chartjs'

  export default {
    extends: Pie,
    props: ["valores"],
    data () {
      return {
        chartData: {
          labels: ["Positivo", "Neutro", "Negativo",],
          datasets: [{
              borderWidth: 2,
              borderColor: [
              'rgba(70, 227, 78, 1)',
              'rgba(54, 162, 235, 1)',
              'rgba(255,99,132,1)',
              
              ],
              backgroundColor: [
              'rgba(70, 227, 78, 0.2)',                
              'rgba(54, 162, 235, 0.2)',
              'rgba(255, 99, 132, 0.2)',
              ],
              data: this.valores,

            }]
        },
        options: {
          legend: {
            display: true
          },
          responsive: true,
          maintainAspectRatio: false
        }
      }
    },
    mounted () {
      this.renderChart(this.chartData, this.options)
    }
  }
</script>