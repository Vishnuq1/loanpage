<!-- 
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
  
  }
  </style>
   -->
   <!-- <template>
    <div class="chart-container">
      <h3>Loan vs Total Payable Amount</h3>
      <canvas ref="loanChartCanvas"></canvas>
    </div>
  </template>
  
  <script>
  import { ref, onMounted, watch, nextTick, onUnmounted } from "vue";
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
        if (!loanChartCanvas.value) return;
        if (chartInstance) chartInstance.destroy(); // Destroy old chart instance
  
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
            maintainAspectRatio: false,
            scales: {
              y: { beginAtZero: true },
            },
          },
        });
      };
  
      watch(
        () => [props.loanAmount, props.totalPayableAmount],
        async () => {
          await nextTick(); // Wait for DOM updates before accessing the canvas
          createChart();
        },
        { immediate: true } // Run on mount too
      );
  
      onMounted(createChart);
  
      onUnmounted(() => {
        if (chartInstance) chartInstance.destroy();
      });
  
      return { loanChartCanvas };
    },
  };
  </script>
  
  <style scoped>
  .chart-container {
    background: white;
    padding: 40px;
    margin-left: 140px;
    border-radius: 8px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  }
  </style>
   -->
<!-- 
   <template>
  <div class="container">
    <div class="calculator-container">
      <form @submit.prevent="calculateEligibility">
        <label>Your Age:</label>
        <input type="number" v-model="age" @input="validateAge" required />
        <span v-if="errors.age" class="error">{{ errors.age }}</span>

        <label>Occupation:</label>
        <select v-model="occupation">
          <option value="Salaried">Salaried</option>
          <option value="Self-Employed">Self-Employed</option>
        </select>

        <label>Monthly Income:</label>
        <input type="number" v-model="monthlyIncome" @input="validateIncome" required />
        <span v-if="errors.monthlyIncome" class="error">{{ errors.monthlyIncome }}</span>

        <label>Existing EMI:</label>
        <input type="number" v-model="existingEMI" @input="validateEMI" required />
        <span v-if="errors.existingEMI" class="error">{{ errors.existingEMI }}</span>

        <label>Rate of Interest (%):</label>
        <input type="number" v-model="interestRate" step="0.1" @input="validateInterestRate" required />
        <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>

        <label>Tenure (Years):</label>
        <select v-model="tenure">
          <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
        </select>

        <button type="submit" :disabled="!isFormValid">Calculate Eligibility</button>
      </form>
    </div>

    <div v-if="eligibilityAmount !== null" class="result-container">
      <div class="result">
        <h3>Eligible Loan Amount: ₹{{ eligibilityAmount }}</h3>
        <h3>Monthly EMI: ₹{{ monthlyEMI }}</h3>
      </div>

      <LoanChart v-if="eligibilityAmount !== null"
        :loanAmount="eligibilityAmount"
        :totalPayableAmount="totalPayableAmount"
      />
    </div>
  </div>
</template>

<script>
import LoanChart from "./LoanChart.vue";

export default {
  components: { LoanChart },
  data() {
    return {
      age: null,
      occupation: "Salaried",
      monthlyIncome: null,
      existingEMI: 0,
      interestRate: 7,
      tenure: 5,
      eligibilityAmount: null,
      monthlyEMI: null,
      totalPayableAmount: null,
      errors: {},
    };
  },
  computed: {
    isFormValid() {
      return !Object.keys(this.errors).length;
    },
  },
  methods: {
    validateAge() {
      if (this.age < 18 || this.age > 70) {
        this.errors.age = "Age must be between 18 and 70.";
      } else {
        delete this.errors.age;
      }
    },
    validateIncome() {
      if (this.monthlyIncome < 30000 || isNaN(this.monthlyIncome)) {
        this.errors.monthlyIncome = "Income must be at least 30,000.";
      } else {
        delete this.errors.monthlyIncome;
      }
    },
    validateEMI() {
      if (this.existingEMI < 0 || isNaN(this.existingEMI)) {
        this.errors.existingEMI = "EMI cannot be negative.";
      } else {
        delete this.errors.existingEMI;
      }
    },
    validateInterestRate() {
      if (this.interestRate < 7 || isNaN(this.interestRate)) {
        this.errors.interestRate = "Interest rate must be at least 7%.";
      } else {
        delete this.errors.interestRate;
      }
    },
    calculateEligibility() {
      if (!this.isFormValid) return;

      const principal = this.monthlyIncome * 60 - this.existingEMI;
      const rate = this.interestRate / 1200;
      const months = this.tenure * 12;

      this.eligibilityAmount = principal;
      this.monthlyEMI = (principal * rate) / (1 - Math.pow(1 + rate, -months));

      this.totalPayableAmount = this.monthlyEMI * months;
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 40px;
  padding: 20px;
}

.calculator-container {
  max-width: 600px;
  padding: 20px;
  border-radius: 12px;
  background: #ffffff;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.result-container {
  width: 400px;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  background: #ffffff;
  text-align: center;
}

.result {
  margin-bottom: 20px;
  font-size: 18px;
  font-weight: bold;
}

button {
  margin-top: 25px;
  width: 100%;
  padding: 15px;
  font-size: 18px;
  background: #007bff;
  color: white;
  border-radius: 8px;
  cursor: pointer;
}

button:hover {
  background: #0056b3;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}
</style> -->

<!-- src/components/LoanChart.vue -->










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
      if (chartInstance) {
        chartInstance.destroy();
      }
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
          maintainAspectRatio: false, // Prevent infinite expansion
          scales: {
            y: { beginAtZero: true },
          },
        },
      });
    };

    watch(
      () => [props.loanAmount, props.totalPayableAmount],
      ([newLoan, newTotal]) => {
        if (chartInstance) {
          chartInstance.data.datasets[0].data = [newLoan, newTotal];
          chartInstance.update(); // Just update, don't re-create
        } else {
          createChart();
        }
      }
    );

    onMounted(createChart);

    return { loanChartCanvas };
  },
};
</script>

<style scoped>
.chart-container {
  width: 400px; /* Set a fixed width */
  height: 350px; /* Set a fixed height */
  overflow: hidden; /* Prevents overflow */
  padding: 20px 20px 25px 20px;
  background: white;
  border-radius: 8px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  margin: auto; /* Centers the chart */
}
</style>

<!-- 

<template>
  <div class="chart-container">
    <h3>Loan vs Total Payable Amount</h3>
    <canvas ref="loanChartCanvas"></canvas>
  </div>
</template>

<script>
import { onMounted, ref, watch, reactive } from "vue";
import Chart from "chart.js/auto";

export default {
  props: {
    loanAmount: Number,
    totalPayableAmount: Number,
  },
  setup(props) {
    const loanChartCanvas = ref(null);
    let chartInstance = null;

    // ✅ Default values for the graph before user input
    const defaultValues = reactive({
      loanAmount: props.loanAmount || 500000, // Default ₹5,00,000
      totalPayableAmount: props.totalPayableAmount || 600000, // Default ₹6,00,000
    });

    const createChart = () => {
      if (chartInstance) {
        chartInstance.destroy();
      }
      chartInstance = new Chart(loanChartCanvas.value, {
        type: "bar",
        data: {
          labels: ["Loan Amount", "Total Payable"],
          datasets: [
            {
              label: "Amount (₹)",
              data: [defaultValues.loanAmount, defaultValues.totalPayableAmount],
              backgroundColor: ["#007bff", "#28a745"],
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            y: { beginAtZero: true },
          },
        },
      });
    };

    // ✅ Watch for prop changes and update the graph
    watch(
      () => [props.loanAmount, props.totalPayableAmount],
      ([newLoan, newTotal]) => {
        if (chartInstance) {
          chartInstance.data.datasets[0].data = [
            newLoan ?? defaultValues.loanAmount,
            newTotal ?? defaultValues.totalPayableAmount,
          ];
          chartInstance.update();
        }
      }
    );

    // ✅ Create the chart with default values on page load
    onMounted(createChart);

    return { loanChartCanvas };
  },
};
</script>

<style scoped>
.chart-container {
  width: 400px;
  height: 350px;
  overflow: hidden;
  padding: 20px 20px 25px 20px;
  background: white;
  border-radius: 8px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  margin: auto;
}
</style> -->
