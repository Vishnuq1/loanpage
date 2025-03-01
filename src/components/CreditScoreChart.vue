<template>
    <div class="chart-container">
      <PieChart :chart-data="chartData" :chart-options="chartOptions" />
    </div>
  </template>
  
  <script>
  import { PieChart } from "vue-chartjs";
  import { Chart as ChartJS, ArcElement, Tooltip, Legend } from "chart.js";
  
  ChartJS.register(ArcElement, Tooltip, Legend);
  
  export default {
    components: { PieChart },
    props: ["score"],
    computed: {
      chartData() {
        return {
          labels: ["Credit Score", "Remaining"],
          datasets: [
            {
              data: [this.score, 900 - this.score],
              backgroundColor: ["#4CAF50", "#ddd"],
            },
          ],
        };
      },
      chartOptions() {
        return {
          responsive: true,
          maintainAspectRatio: false,
        };
      },
    },
  };
  </script>
  
  <style scoped>
  .chart-container {
    width: 300px;
    height: 300px;
    margin: auto;
  }
  </style>
  