
   <template>
  
  <h2></h2>

 
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
          <option v-for="year in 26" :key="year" :value="year+4">{{ year+4 }}</option>
        </select>
    
        <button type="submit" :disabled="!isFormValid">Calculate Eligibility</button>
      </form>
    </div>

    <!-- right side eligibility and chart -->
      <div v-if="eligibilityAmount !== null" class="result">
        <div class="resule">
        <h3>Eligible Loan Amount: ₹{{ eligibilityAmount }}</h3>
        <h3>Monthly EMI: ₹{{ monthlyEMI }}</h3>
      </div>
  
      <!-- LoanChart Component (Showing Graph) -->
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
        totalPayableAmount: null, // NEW: Total Amount after Interest
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
  
        // Calculate Loan Eligibility
        const principal = (this.monthlyIncome * 60) - this.existingEMI;
        const rate = this.interestRate / 1200;
        const months = this.tenure * 12;
  
        this.eligibilityAmount = principal;
        this.monthlyEMI = (principal * rate) / (1 - Math.pow(1 + rate, -months));
  
        // Calculate Total Payable Amount (Loan + Interest)
        this.totalPayableAmount = this.monthlyEMI * months;
      },
    },
  };
  </script>
  
  <style>
  .container {
  display: flex;
  justify-content: space-between; /* Puts form & results side by side */
  align-items: flex-start;
  gap: 40px; /* Adds spacing between form and results */
  padding: 20px;
}
  .calculator-container {
    font-family: 'Poppins', sans-serif;  
    /* display: flex; */
    /* justify-content: space-between; */
    /* align-items: flex-start; */
    /* padding: 20px; */
    border: 1px solid #ccc;
    /* border-radius: 10px; */
    /* background: #f9f9f9; */
    max-width: 1000px;  /* Increase max width */
    min-width: 700px; 
   
  margin: auto;
  padding: 45px;
  border-radius: 12px;
  /* background: #ffffff; */
  /* box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1); */
  text-align: center;
  /* font-family: "Roboto", sans-serif; */
  }
  .result-container {
  width: 45%; /* Adjust results width */
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

  label {
  font-size: 18px;  /* Bigger labels */
  font-weight: 600; 
  margin-bottom: 8px;
}

input, select {
  width: 100%;
  padding: 14px;  /* Increased padding */
  font-size: 16px; /* Bigger text */
  border-radius: 8px;
  border: 2px solid #ccc;
  transition: all 0.3s ease;
  text-align: center; /* Centers the entered/select text */
}
  /* label, input, select, button {
    display: block;
    width: 100%;
    margin-bottom: 10px;
  } */
  /* input:focus, select:focus {
  border-color: #007bff;
  box-shadow: 0px 0px 10px rgba(0, 123, 255, 0.3);
} */
  /* .eligibility_header{
    display:flex;
  } */
  /* button {
    background: blue;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
  }
  
  .error {
    color: red;
  }
  
  .result {
    margin-top: 20px;
  }
   */
  /* .chart-container {
    flex: 1;
  } */
  button {
    margin-top:25px;
  width: 100%;
  padding: 15px;  /* Bigger button */
  font-size: 20px; /* Larger text */
  font-weight:light;
  background: #007bff;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:hover {
  background: #0056b3;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}
  </style>
  