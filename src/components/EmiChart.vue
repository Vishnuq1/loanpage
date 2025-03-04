<!-- <template>
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
   -->



   <!-- <template>
    <div class="chart-container">
      <h3>Principal vs. Interest</h3>
      <canvas ref="chartCanvas"></canvas>
    </div>
  </template>
  
  <script>
  import { ref, onMounted, watch, nextTick } from "vue";
  import Chart from "chart.js/auto";
  
  export default {
    props: {
      loanAmount: Number,
      totalPayable: Number,
    },
    setup(props) {
      const chartCanvas = ref(null);
      let chartInstance = null;
  
      const createChart = async () => {
        if (!props.loanAmount || !props.totalPayable) return; // Ensure values exist
        if (chartInstance) chartInstance.destroy(); // Destroy previous chart
  
        const interestAmount = props.totalPayable - props.loanAmount;
  
        await nextTick(); // Wait for DOM update
  
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
            maintainAspectRatio: false, // Helps in resizing
          },
        });
      };
  
      watch(() => [props.loanAmount, props.totalPayable], createChart, { immediate: true });
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
   -->




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
      totalPayable: Number, // ✅ Corrected prop name to match parent
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
  