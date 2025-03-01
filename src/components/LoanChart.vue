<!--  src/components/LoanChart.vue -->
<template>
    <div class="chart-container">
      <h3>Loan vs Total Payable Amount</h3>
      <canvas ref="loanChartCanvas"></canvas>
    </div>
  </template>
  
  <script>
  import { onMounted, ref, watch } from "vue";
  import Chart from "chart.js/auto";
  
  export default {
    props: {
      loanAmount: Number,
      totalPayableAmount: Number,
    },
    setup(props) {
      const loanChartCanvas = ref(null);
      let chartInstance = null;
  
      const createChart = () => {
        if (chartInstance) chartInstance.destroy();
        chartInstance = new Chart(loanChartCanvas.value, {
          type: "bar",
          data: {
            labels: ["Loan Amount", "Total Payable"],
            datasets: [
              {
                label: "Amount (₹)",
                data: [props.loanAmount, props.totalPayableAmount],
                backgroundColor: ["#007bff", "#28a745"],
              },
            ],
          },
          options: {
            responsive: true,
            scales: {
              y: { beginAtZero: true },
            },
          },
        });
      };
  
      watch(() => [props.loanAmount, props.totalPayableAmount], createChart);
      onMounted(createChart);
  
      return { loanChartCanvas };
    },
  };
  </script>
  
  <style scoped>
  .chart-container {
    background: white;
    padding: 40px;
    margin-left:140px;
    border-radius: 8px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
    /* text-align: center; */
  }
  </style>
  