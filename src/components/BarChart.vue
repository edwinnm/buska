<script>
  import { Bar } from 'vue-chartjs'

  export default {
    extends: Bar,
    props: {
      datos:{type: Object},
      cambia: {type: String}
    },
    watch: {
    chartData() {
      this.renderChart(this.chartData, this.chartOptions);
    },
      // datos:{
        
      //   handler(val){
      //     console.log("cambiando al mundo " +val)
      //   },
      //   deep: true,
        
      // },
      cambia:function(){
          this.chartData.datasets[0].data = this.datos.ml
          this.chartData.datasets[1].data = this.datos.ebay
          this.chartData.datasets[2].data = this.datos.olx
          this.$data._chart.update()
          // this.renderChart(this.chartData, this.chartOptions)
      }
    },
    data() {
      return {
        chartData: {
          labels: ['Maximo','Promedio','Minimo'],
          datasets: [{
            label: ['Mercado Libre'],
            borderWidth: 1,
            backgroundColor: [
              'rgba(255, 206, 86, 0.2)',
              'rgba(255, 206, 86, 0.2)',
              'rgba(255, 206, 86, 0.2)',
            ],
            borderColor: [
              'rgba(255, 206, 86, 1)',
              'rgba(255, 206, 86, 1)',
              'rgba(255, 206, 86, 1)',

            ],
            pointBorderColor: '#2554FF',
            data: [0,0,0]
          },
          {
            label: ['Ebay'],
            borderWidth: 1,
            backgroundColor: [
              'rgba(54, 162, 235, 0.2)',
              'rgba(54, 162, 235, 0.2)',
              'rgba(54, 162, 235, 0.2)',
            ],
            borderColor: [
              'rgba(54, 162, 235, 1)',
              'rgba(54, 162, 235, 1)',
              'rgba(54, 162, 235, 1)',

            ],
            pointBorderColor: '#2554FF',
            data: [0,0,0]
          },
          {
            label: ['Olx'],
            borderWidth: 1,
            backgroundColor: [
              'rgba(89, 211, 77, 0.2)',
              'rgba(89, 211, 77, 0.2)',
              'rgba(89, 211, 77, 0.2)',
            ],
            borderColor: [
              'rgba(89, 211, 77, 1)',
              'rgba(89, 211, 77, 1)',
              'rgba(89, 211, 77, 1)',

            ],
            pointBorderColor: '#2554FF',
            data: [0,0,0]
          },
          
          ]
        },
        options: {
          scales: {
            yAxes: [{
              ticks: {
                beginAtZero: true
              },
              gridLines: {
                display: true
              }
            }],
            xAxes: [{
              gridLines: {
                display: false
              }
            }]
          },
          legend: {
            display: true
          },
        responsive: true, 
        maintainAspectRatio: false, 
        }
      }
    },
    mounted() {
      this.chartData.datasets[0].data = this.datos.ml
      this.chartData.datasets[1].data = this.datos.ebay
      this.chartData.datasets[2].data = this.datos.olx
      this.renderChart(this.chartData, this.options)
    },

  

  }
</script>