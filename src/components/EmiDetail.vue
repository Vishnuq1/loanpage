<!-- <template>
    <div class="calculator-container">
      <h2>Loan EMI Calculator</h2>
  
      <form @submit.prevent="calculateEMI">
        <label>Loan Amount (₹):</label>
        <input type="number" v-model="loanAmount" required @input="validateLoanAmount" />
        <span v-if="errors.loanAmount" class="error">{{ errors.loanAmount }}</span>
  
        <label>Tenure (Years):</label>
        <select v-model="tenure">
          <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
        </select>
  
        <label>Interest Rate (%):</label>
        <input type="number" v-model="interestRate" step="0.1" required @input="validateInterestRate" />
        <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
  
        <button type="submit" :disabled="!isFormValid">Calculate EMI</button>
      </form>
  
      <div v-if="emi !== null" class="result">
        <h3>Monthly EMI: ₹{{ emi.toFixed(2) }}</h3>
        <h3>Total Payable Amount: ₹{{ totalPayable.toFixed(2) }}</h3>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        loanAmount: null,
        tenure: 10,
        interestRate: 7,
        emi: null,
        totalPayable: null,
        errors: {},
      };
    },
    computed: {
      isFormValid() {
        return !Object.keys(this.errors).length;
      },
    },
    methods: {
      validateLoanAmount() {
        if (this.loanAmount < 100000 || this.loanAmount > 10000000000 || isNaN(this.loanAmount)) {
          this.errors.loanAmount = "Loan amount must be between ₹1,00,000 and ₹100 crore.";
        } else {
          delete this.errors.loanAmount;
        }
      },
      validateInterestRate() {
        if (this.interestRate < 7 || isNaN(this.interestRate)) {
          this.errors.interestRate = "Interest rate must be at least 7%.";
        } else {
          delete this.errors.interestRate;
        }
      },
      calculateEMI() {
        if (!this.isFormValid) return;
  
        const P = this.loanAmount;
        const r = this.interestRate / 1200;
        const n = this.tenure * 12;
  
        this.emi = (P * r) / (1 - Math.pow(1 + r, -n));
        this.totalPayable = this.emi * n;
  
        this.$emit("emi-calculated", { loanAmount: this.loanAmount, totalPayable: this.totalPayable });
      },
    },
  };
  </script>
  
  <style scoped>
  .calculator-container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  label {
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 8px;
    display: block;
  }
  input, select {
    width: 100%;
    padding: 12px;
    font-size: 16px;
    border-radius: 8px;
    border: 2px solid #ccc;
    margin-bottom: 10px;
  }
  button {
    width: 100%;
    padding: 12px;
    font-size: 18px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  .error {
    color: red;
  }
  </style>
   -->



   <!-- <template>
    <div class="calculator-container">
      <h2>Loan EMI Calculator</h2>
  
      <form @submit.prevent="calculateEMI">
        <div class="input-group">
          <div class="input-field">
            <label>Loan Amount (₹):</label>
            <input type="number" v-model="loanAmount" required @input="validateLoanAmount" />
            <span v-if="errors.loanAmount" class="error">{{ errors.loanAmount }}</span>
          </div>
  
          <div class="input-field">
            <label>Tenure (Years):</label>
            <select v-model="tenure">
              <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
            </select>
          </div>
  
          <div class="input-field">
            <label>Interest Rate (%):</label>
            <input type="number" v-model="interestRate" step="0.1" required @input="validateInterestRate" />
            <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
          </div>
        </div>
  
        <button type="submit" :disabled="!isFormValid">Calculate EMI</button>
      </form>
  
      <div v-if="emi !== null" class="result">
        <h3>Monthly EMI: ₹{{ emi.toFixed(2) }}</h3>
        <h3>Total Payable Amount: ₹{{ totalPayable.toFixed(2) }}</h3>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        loanAmount: null,
        tenure: 10,
        interestRate: 7,
        emi: null,
        totalPayable: null,
        errors: {},
      };
    },
    computed: {
      isFormValid() {
        return !Object.keys(this.errors).length;
      },
    },
    methods: {
      validateLoanAmount() {
        if (this.loanAmount < 100000 || this.loanAmount > 10000000000 || isNaN(this.loanAmount)) {
          this.errors.loanAmount = "Loan amount must be between ₹1,00,000 and ₹100 crore.";
        } else {
          delete this.errors.loanAmount;
        }
      },
      validateInterestRate() {
        if (this.interestRate < 7 || isNaN(this.interestRate)) {
          this.errors.interestRate = "Interest rate must be at least 7%.";
        } else {
          delete this.errors.interestRate;
        }
      },
      calculateEMI() {
        if (!this.isFormValid) return;
  
        const P = this.loanAmount;
        const r = this.interestRate / 1200;
        const n = this.tenure * 12;
  
        this.emi = (P * r) / (1 - Math.pow(1 + r, -n));
        this.totalPayable = this.emi * n;
  
        this.$emit("emi-calculated", { loanAmount: this.loanAmount, totalPayable: this.totalPayable });
      },
    },
  };
  </script>
  
  <style scoped>
  .calculator-container {
    max-width: 700px;
    margin: auto;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  
  /* Make inputs appear in a row */
  .input-group {
    display: flex;
    gap: 10px;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .input-field {
    flex: 1;
  }
  
  /* Adjust input & select styling */
  input, select {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 6px;
    border: 2px solid #ccc;
  }
  
  /* Button styling */
  button {
    width: 100%;
    padding: 12px;
    font-size: 18px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  
  button:disabled {
    background: gray;
    cursor: not-allowed;
  }
  
  /* Error styling */
  .error {
    color: red;
    font-size: 14px;
    display: block;
    margin-top: 5px;
  }
  </style>
   -->

<!-- 
   <template>
    <div class="calculator-container">
      <h2>Loan EMI Calculator</h2>
  
      <form @submit.prevent="calculateEMI">
        <div class="input-group">
          <div class="input-field">
            <label>Loan Amount (₹):</label>
            <input type="number" v-model="loanAmount" required @input="validateLoanAmount" />
            <span v-if="errors.loanAmount" class="error">{{ errors.loanAmount }}</span>
          </div>
  
          <div class="input-field">
            <label>Tenure (Years):</label>
            <select v-model="tenure">
              <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
            </select>
          </div>
  
          <div class="input-field">
            <label>Interest Rate (%):</label>
            <input type="number" v-model="interestRate" step="0.1" required @input="validateInterestRate" />
            <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
          </div>
        </div>
  
        <button type="submit" :disabled="!isFormValid">Calculate EMI</button>
      </form>
  
      <div v-if="emi !== null" class="result">
        <h3>Monthly EMI: ₹{{ emi.toFixed(2) }}</h3>
        <h3>Total Payable Amount: ₹{{ totalPayable.toFixed(2) }}</h3>
      </div>
  
      <LoanChart v-if="emi !== null" :loanAmount="loanAmount" :totalPayableAmount="totalPayable" />
    </div>
  </template>
  
  <script>
  import EmiChart from "./EmiChart.vue";
  
  export default {
    components: { EmiChart },
    data() {
      return {
        loanAmount: null,
        tenure: 10,
        interestRate: 7,
        emi: null,
        totalPayable: null,
        errors: {},
      };
    },
    computed: {
      isFormValid() {
        return !Object.keys(this.errors).length;
      },
    },
    methods: {
      validateLoanAmount() {
        if (this.loanAmount < 100000 || this.loanAmount > 10000000000 || isNaN(this.loanAmount)) {
          this.errors.loanAmount = "Loan amount must be between ₹1,00,000 and ₹100 crore.";
        } else {
          delete this.errors.loanAmount;
        }
      },
      validateInterestRate() {
        if (this.interestRate < 7 || isNaN(this.interestRate)) {
          this.errors.interestRate = "Interest rate must be at least 7%.";
        } else {
          delete this.errors.interestRate;
        }
      },
      calculateEMI() {
        if (!this.isFormValid) return;
  
        const P = this.loanAmount;
        const r = this.interestRate / 1200;
        const n = this.tenure * 12;
  
        this.emi = (P * r) / (1 - Math.pow(1 + r, -n));
        this.totalPayable = this.emi * n;
      },
    },
  };
  </script>
  
  <style scoped>
  .calculator-container {
    max-width: 700px;
    margin: auto;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  
 
  .input-group {
    display: flex;
    gap: 10px;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .input-field {
    flex: 1;
  }
  
  input, select {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 6px;
    border: 2px solid #ccc;
  }
  
  button {
    width: 100%;
    padding: 12px;
    font-size: 18px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  
  button:disabled {
    background: gray;
    cursor: not-allowed;
  }
  
  .error {
    color: red;
    font-size: 14px;
    display: block;
    margin-top: 5px;
  }
  </style>
   -->





   <template>
<h1 class="emiheading">
  Calculate <span class="bold-emi">EMI</span>
</h1>
<h1 class="subheading">For the Loan Amount You Require</h1>

    <div class="calculator-container">
      <h2>Loan EMI Calculator</h2>
  
      <form @submit.prevent="calculateEMI">
        <div class="input-group">
          <div class="input-field">
            <label>Loan Amount (₹):</label>
            <input type="number" v-model="loanAmount" required @input="validateLoanAmount" />
            <span v-if="errors.loanAmount" class="error">{{ errors.loanAmount }}</span>
          </div>
  
          <div class="input-field">
            <label>Tenure (Years):</label>
            <select v-model="tenure">
              <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
            </select>
          </div>
  
          <div class="input-field">
            <label>Interest Rate (%):</label>
            <input type="number" v-model="interestRate" step="0.1" required @input="validateInterestRate" />
            <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
          </div>
        </div>
  
        <button type="submit" :disabled="!isFormValid">Calculate EMI</button>
      </form>
  
      <div v-if="emi !== null" class="result">
        <h3>Monthly EMI: ₹{{ emi.toFixed(2) }}</h3>
        <h3>Total Payable Amount: ₹{{ totalPayable.toFixed(2) }}</h3>
      </div>
  

      <EmiChart v-if="emi !== null" :loanAmount="loanAmount" :totalPayable="totalPayable" />
    </div>
  </template>
  
  <script>
  import EmiChart from "./EmiChart.vue"; // ✅ Correct import
  
  export default {
    components: { EmiChart },
    data() {
      return {
        loanAmount: null,
        tenure: 10,
        interestRate: 7,
        emi: null,
        totalPayable: null,
        errors: {},
      };
    },
    computed: {
      isFormValid() {
        return !Object.keys(this.errors).length;
      },
    },
    methods: {
      validateLoanAmount() {
        if (this.loanAmount < 100000 || this.loanAmount > 10000000000 || isNaN(this.loanAmount)) {
          this.errors.loanAmount = "Loan amount must be between ₹1,00,000 and ₹100 crore.";
        } else {
          delete this.errors.loanAmount;
        }
      },
      validateInterestRate() {
        if (this.interestRate < 7 || isNaN(this.interestRate)) {
          this.errors.interestRate = "Interest rate must be at least 7%.";
        } else {
          delete this.errors.interestRate;
        }
      },
      calculateEMI() {
        if (!this.isFormValid) return;
  
        const P = this.loanAmount;
        const r = this.interestRate / 1200;
        const n = this.tenure * 12;
  
        this.emi = (P * r) / (1 - Math.pow(1 + r, -n));
        this.totalPayable = this.emi * n;
      },
    },
  };
  </script>
  
  <style scoped>

  /* .emiheading {

  bottom: 0;
  left: 0;
  padding: 10px;
  text-align: left;
  margin-bottom: 10px;
} */
.emiheading {
  font-size: 28px; /* Adjust size if needed */
  font-weight: normal;
  text-align: left; /* Align text to the left */
  line-height: 1; /* Remove extra space */
  margin-bottom: 10px; /* Remove bottom margin */
  margin-left: 10px; /* Adjust left margin if needed */
}

.bold-emi {
  font-weight: 600; /* Extra thick EMI */
}

.subheading {
  font-size: 24px; /* Adjust size if needed */
  font-weight: normal;
  text-align: left; /* Align text to the left */
  margin-top: 0; /* Remove top margin */
  line-height: 1; /* Ensures no extra space */
  margin-left: 10px; /* Adjust left margin if needed */
  margin-bottom: 10px;
}



  .calculator-container {
    max-width: 700px;
    /* margin: auto; */
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    margin-left: 0;
   
  }
  
  .input-group {
    display: flex;
    gap: 10px;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .input-field {
    flex: 1;
  }
  
  input, select {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 6px;
    border: 2px solid #ccc;
  }
  
  button {
    width: 100%;
    padding: 12px;
    font-size: 18px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  
  button:disabled {
    background: gray;
    cursor: not-allowed;
  }
  
  .error {
    color: red;
    font-size: 14px;
    display: block;
    margin-top: 5px;
  }
  </style>
  