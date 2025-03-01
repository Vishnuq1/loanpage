<template>
    <div class="chart-container">
      <h3>Principal vs. Interest</h3>
      <canvas ref="chartCanvas"></canvas>
    </div>
  </template>
  
  <script>
  import { ref, onMounted, watch } from "vue";
  import Chart from "chart.js/auto";
  
  export default {
    props: {
      loanAmount: Number,
      totalPayable: Number,
    },
    setup(props) {
      const chartCanvas = ref(null);
      let chartInstance = null;
  
      const createChart = () => {
        if (chartInstance) chartInstance.destroy();
  
        const interestAmount = props.totalPayable - props.loanAmount;
  
        chartInstance = new Chart(chartCanvas.value, {
          type: "pie",
          data: {
            labels: ["Principal Amount", "Total Interest"],
            datasets: [
              {
                data: [props.loanAmount, interestAmount],
                backgroundColor: ["#007bff", "#ffcc00"],
              },
            ],
          },
          options: {
            responsive: true,
          },
        });
      };
  
      watch(() => [props.loanAmount, props.totalPayable], createChart);
      onMounted(createChart);
  
      return { chartCanvas };
    },
  };
  </script>
  
  <style scoped>
  .chart-container {
    max-width: 400px;
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  </style>
  