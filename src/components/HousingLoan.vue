<!-- 
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


      <div v-if="eligibilityAmount !== null" class="result">
        <div class="resule">
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
      age: 18,
      occupation: "Salaried",
      monthlyIncome: 30000,
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

      const netIncome = this.monthlyIncome - this.existingEMI;
      const maxEMI = netIncome * 0.5; // Assuming 50% income can go to EMI

      // Loan Calculation Formula (EMI)
      const rate = this.interestRate / 1200;
      const months = this.tenure * 12;
      this.eligibilityAmount = (maxEMI * (1 - Math.pow(1 + rate, -months))) / rate;
      
      // Monthly EMI Calculation
      this.monthlyEMI = (this.eligibilityAmount * rate) / (1 - Math.pow(1 + rate, -months));

      // Total Payable Amount (Loan + Interest)
      this.totalPayableAmount = this.monthlyEMI * months;
    },
  },
};
</script>

  
  
  <style>
  .container {
  display: flex;
  justify-content: space-between; 
  align-items: flex-start;
  gap: 40px; 
  padding: 20px;
}
  .calculator-container {
    font-family: 'Poppins', sans-serif;  
    
    border: 1px solid #ccc;

    max-width: 1000px; 
    min-width: 700px; 
   
  margin: auto;
  padding: 45px;
  border-radius: 12px;
  
  text-align: center;

  }
  .result-container {
  width: 45%;
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
  font-size: 18px;  
  font-weight: 600; 
  margin-bottom: 8px;
}

input, select {
  width: 100%;
  padding: 14px;  
  font-size: 16px; 
  border-radius: 8px;
  border: 2px solid #ccc;
  transition: all 0.3s ease;
  text-align: center;
}
 
  button {
    margin-top:25px;
  width: 100%;
  padding: 15px; 
  font-size: 20px; 
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
   -->

   <!-- <template>
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
  </style>
   -->
<!-- 
   <template>
    <div class="loan-container">
      <div class="loan-calculator">
        <h2 class="title">Housing Loan Eligibility Calculator</h2>
  
        <form @submit.prevent="calculateEligibility">
          <div class="input-group">
            <label>Your Age:</label>
            <input type="number" v-model="age" @input="validateAge" required />
            <span v-if="errors.age" class="error">{{ errors.age }}</span>
          </div>
  
          <div class="input-group">
            <label>Occupation:</label>
            <select v-model="occupation">
              <option value="Salaried">Salaried</option>
              <option value="Self-Employed">Self-Employed</option>
            </select>
          </div>
  
          <div class="input-group">
            <label>Monthly Income:</label>
            <input type="number" v-model="monthlyIncome" @input="validateIncome" required />
            <span v-if="errors.monthlyIncome" class="error">{{ errors.monthlyIncome }}</span>
          </div>
  
          <div class="input-group">
            <label>Existing EMI:</label>
            <input type="number" v-model="existingEMI" @input="validateEMI" required />
            <span v-if="errors.existingEMI" class="error">{{ errors.existingEMI }}</span>
          </div>
  
          <div class="input-group">
            <label>Rate of Interest (%):</label>
            <input type="number" v-model="interestRate" step="0.1" @input="validateInterestRate" required />
            <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
          </div>
  
          <div class="input-group">
            <label>Tenure (Years):</label>
            <select v-model="tenure">
              <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
            </select>
          </div>
  
          <button type="submit" :disabled="!isFormValid" class="calculate-btn">Calculate Eligibility</button>
        </form>
      </div>
  
      <div v-if="eligibilityAmount !== null" class="loan-result">
        <h3 class="result-title">Loan Eligibility Result</h3>
        <p><strong>Eligible Loan Amount:</strong> ₹{{ eligibilityAmount }}</p>
        <p><strong>Monthly EMI:</strong> ₹{{ monthlyEMI }}</p>
  
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
        this.errors.age = this.age < 18 || this.age > 70 ? "Age must be between 18 and 70." : "";
      },
      validateIncome() {
        this.errors.monthlyIncome = this.monthlyIncome < 30000 ? "Income must be at least 30,000." : "";
      },
      validateEMI() {
        this.errors.existingEMI = this.existingEMI < 0 ? "EMI cannot be negative." : "";
      },
      validateInterestRate() {
        this.errors.interestRate = this.interestRate < 7 ? "Interest rate must be at least 7%." : "";
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
  .loan-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px;
    padding: 20px;
    max-width: 700px;
    margin: auto;
  }
  
  .loan-calculator {
    width: 100%;
    background: #fff;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.1);
  }
  
  .title {
    text-align: center;
    font-size: 22px;
    color: #333;
    margin-bottom: 15px;
  }
  
  .input-group {
    display: flex;
    flex-direction: column;
    margin-bottom: 12px;
  }
  
  .input-group label {
    font-weight: 600;
    color: #555;
    margin-bottom: 5px;
  }
  
  .input-group input,
  .input-group select {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 16px;
    transition: 0.3s ease-in-out;
  }
  
  .input-group input:focus,
  .input-group select:focus {
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
    outline: none;
  }
  
  .error {
    color: #ff4d4d;
    font-size: 14px;
    margin-top: 5px;
  }
  
  .calculate-btn {
    background: linear-gradient(45deg, #007bff, #0056b3);
    color: white;
    font-size: 18px;
    padding: 12px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.3s;
    width: 100%;
    margin-top: 15px;
  }
  
  .calculate-btn:hover {
    background: linear-gradient(45deg, #0056b3, #003c80);
  }
  
  .calculate-btn:disabled {
    background: #ddd;
    cursor: not-allowed;
  }
  
  .loan-result {
    background: #f9f9f9;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .result-title {
    font-size: 20px;
    color: #007bff;
    margin-bottom: 10px;
  }
  
  .loan-result p {
    font-size: 18px;
    color: #333;
  }
  </style>
   -->




















<!-- 
   <template>
    <h1 class="housingheading">Calculate Housing Loan Eligibility</h1>
    <div class="housing-loan-calculator">
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
          <h3>Eligible Loan Amount: ₹{{ eligibilityAmount.toLocaleString() }}</h3>
          <h3>Monthly EMI: ₹{{ monthlyEMI.toFixed(2).toLocaleString() }}</h3>
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
        errors: {}, // Ensuring reactivity
      };
    },
    computed: {
      isFormValid() {
        return Object.keys(this.errors).length === 0;
      },
    },
    methods: {
      validateAge() {
        if (!this.age || this.age < 18 || this.age > 70) {
          this.errors.age = "Age must be between 18 and 70.";
        } else {
          delete this.errors.age;
        }
      },
  
      validateIncome() {
        if (!this.monthlyIncome || this.monthlyIncome < 30000) {
          this.errors.monthlyIncome = "Income must be at least ₹30,000.";
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
        console.log("Button clicked, checking form validity...");
        if (!this.isFormValid) {
          console.log("Form is invalid:", this.errors);
          return;
        }
  
        console.log("Form is valid, calculating eligibility...");
        const principal = this.monthlyIncome * 60 - this.existingEMI;
        const rate = this.interestRate / 1200;
        const months = this.tenure * 12;
  
        if (rate === 0) {
          console.error("Interest rate cannot be zero.");
          return;
        }
  
        this.eligibilityAmount = Math.max(principal, 0); // Ensuring positive value
        this.monthlyEMI = (principal * rate) / (1 - Math.pow(1 + rate, -months));
        this.totalPayableAmount = this.monthlyEMI * months;
  
        console.log("Loan Eligibility Calculated:", this.eligibilityAmount, "EMI:", this.monthlyEMI);
      },
    },
  };
  </script>
  
  <style scoped>
  .housingheading{
    text-align: left;
    margin-bottom: 15px;
    margin-left: 20px;
  }

  .housing-loan-calculator {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    padding: 20px;
    min-width: 500px;
    /* justify-content: left; */
  }
  
  .calculator-container {
    width: 100%;
    max-width: 500px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    display: grid;
  grid-template-columns: repeat(2, 1fr); /* Two columns */
  grid-template-rows: repeat(2, auto); /* Two rows */
  gap: 15px; /* Adds space between fields */
  }
  .full-width {
  grid-column: span 2;
}
.form-group {
  display: flex;
  flex-direction: column;
}

  
  .result-container {
    width: 100%;
    max-width: 400px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .result {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  input, select {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 6px;
    border: 1px solid #ccc;
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
    grid-column: span 2;
  }
  
  button:hover {
    background: #0056b3;
  }
  
  button:disabled {
    background: #ccc;
    cursor: not-allowed;
  }
  
  .error {
    color: red;
    font-size: 14px;
  }

 


  </style>
   -->



   <!-- <template>
    <h1 class="housingheading">Calculate Housing Loan Eligibility</h1>
    <div class="housing-loan-calculator">
      <div class="calculator-container">
        <form @submit.prevent="calculateEligibility">
          <div class="grid-container">
            <div class="form-group">
              <label>Your Age:</label>
              <input type="number" v-model="age" @input="validateAge" required />
              <span v-if="errors.age" class="error">{{ errors.age }}</span>
            </div>
  
            <div class="form-group">
              <label>Occupation:</label>
              <select v-model="occupation">
                <option value="Salaried">Salaried</option>
                <option value="Self-Employed">Self-Employed</option>
              </select>
            </div>
  
            <div class="form-group">
              <label>Monthly Income:</label>
              <input type="number" v-model="monthlyIncome" @input="validateIncome" required />
              <span v-if="errors.monthlyIncome" class="error">{{ errors.monthlyIncome }}</span>
            </div>
  
            <div class="form-group">
              <label>Existing EMI:</label>
              <input type="number" v-model="existingEMI" @input="validateEMI" required />
              <span v-if="errors.existingEMI" class="error">{{ errors.existingEMI }}</span>
            </div>
  
            <div class="form-group">
              <label>Rate of Interest (%):</label>
              <input type="number" v-model="interestRate" step="0.1" @input="validateInterestRate" required />
              <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
            </div>
  
            <div class="form-group">
              <label>Tenure (Years):</label>
              <select v-model="tenure">
                <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
              </select>
            </div>
          </div>
  
          <button type="submit" :disabled="!isFormValid">Calculate Eligibility</button>
        </form>
      </div>
  
      <div v-if="eligibilityAmount !== null" class="result-container">
        <div class="result">
          <h3>Eligible Loan Amount: ₹{{ eligibilityAmount.toLocaleString() }}</h3>
          <h3>Monthly EMI: ₹{{ monthlyEMI.toFixed(2).toLocaleString() }}</h3>
        </div>
  
        <LoanChart
          v-if="eligibilityAmount !== null"
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
        errors: {}, // Ensuring reactivity
      };
    },
    computed: {
      isFormValid() {
        return Object.keys(this.errors).length === 0;
      },
    },
    methods: {
      validateAge() {
        if (!this.age || this.age < 18 || this.age > 70) {
          this.errors.age = "Age must be between 18 and 70.";
        } else {
          delete this.errors.age;
        }
      },
  
      validateIncome() {
        if (!this.monthlyIncome || this.monthlyIncome < 30000) {
          this.errors.monthlyIncome = "Income must be at least ₹30,000.";
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
        console.log("Button clicked, checking form validity...");
        if (!this.isFormValid) {
          console.log("Form is invalid:", this.errors);
          return;
        }
  
        console.log("Form is valid, calculating eligibility...");
        const principal = this.monthlyIncome * 60 - this.existingEMI;
        const rate = this.interestRate / 1200;
        const months = this.tenure * 12;
  
        if (rate === 0) {
          console.error("Interest rate cannot be zero.");
          return;
        }
  
        this.eligibilityAmount = Math.max(principal, 0); // Ensuring positive value
        this.monthlyEMI = (principal * rate) / (1 - Math.pow(1 + rate, -months));
        this.totalPayableAmount = this.monthlyEMI * months;
  
        console.log("Loan Eligibility Calculated:", this.eligibilityAmount, "EMI:", this.monthlyEMI);
      },
    },
  };
  </script>
  
  <style scoped>
  .housingheading {
    text-align: left;
    margin-bottom: 15px;
    margin-left: 20px;
  }
  
  .housing-loan-calculator {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    padding: 20px;
    min-width: 600px;
  }
  
  .calculator-container {
    width: 100%;
    max-width: 600px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    height:400px;
  }
  
  .grid-container {
    margin-top: 10px;
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* Three columns */
    grid-template-rows: repeat(2, auto); /* Two rows */
    gap: 25px; /* Adds space between fields */
  }
  
  .form-group {
    display: flex;
    flex-direction: column;
  }
  
  .result-container {
    width: 100%;
    max-width: 460px;
    height:100px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .result {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  input,
  select {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border-radius: 6px;
    border: 1px solid #ccc;
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
    margin-top: 30px;
  }
  
  button:hover {
    background: #0056b3;
  }
  
  button:disabled {
    background: #ccc;
    cursor: not-allowed;
  }
  
  .error {
    color: red;
    font-size: 14px;
  }
  </style>
   -->
  

   <!-- <template>
    <h1 class="housingheading">Calculate Housing Loan Eligibility</h1>
    <div class="housing-loan-calculator">
      <div class="calculator-container">
        <form @submit.prevent="calculateEligibility">
          <div class="grid-container">
            <div class="form-group">
              <label>Your Age:</label>
              <input type="number" v-model="age" @input="validateAge" required />
              <span v-if="errors.age" class="error">{{ errors.age }}</span>
            </div>
  
            <div class="form-group">
              <label>Occupation:</label>
              <select v-model="occupation">
                <option value="Salaried">Salaried</option>
                <option value="Self-Employed">Self-Employed</option>
              </select>
            </div>
  
            <div class="form-group">
              <label>Monthly Income:</label>
              <input type="number" v-model="monthlyIncome" @input="validateIncome" required />
              <span v-if="errors.monthlyIncome" class="error">{{ errors.monthlyIncome }}</span>
            </div>
  
            <div class="form-group">
              <label>Existing EMI:</label>
              <input type="number" v-model="existingEMI" @input="validateEMI" required />
              <span v-if="errors.existingEMI" class="error">{{ errors.existingEMI }}</span>
            </div>
  
            <div class="form-group">
              <label>Rate of Interest (%):</label>
              <input type="number" v-model="interestRate" step="0.1" @input="validateInterestRate" required />
              <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
            </div>
  
            <div class="form-group">
              <label>Tenure (Years):</label>
              <select v-model="tenure">
                <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
              </select>
            </div>
          </div>
  
          <button type="submit" :disabled="!isFormValid">Calculate Eligibility</button>
        </form>
      </div>
  
      <div v-if="eligibilityAmount !== null" class="result-container">
        <div class="result">
          <h3>Eligible Loan Amount: ₹{{ eligibilityAmount.toLocaleString() }}</h3>
          <h3>Monthly EMI: ₹{{ monthlyEMI.toFixed(2).toLocaleString() }}</h3>
        </div>
  
        <LoanChart
          v-if="eligibilityAmount !== null"
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
        errors: {}, // Ensuring reactivity
      };
    },
    computed: {
      isFormValid() {
        return Object.keys(this.errors).length === 0;
      },
    },
    methods: {
      validateAge() {
        if (!this.age || this.age < 18 || this.age > 70) {
          this.errors.age = "Age must be between 18 and 70.";
        } else {
          delete this.errors.age;
        }
      },
  
      validateIncome() {
        if (!this.monthlyIncome || this.monthlyIncome < 30000) {
          this.errors.monthlyIncome = "Income must be at least ₹30,000.";
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
        console.log("Button clicked, checking form validity...");
        if (!this.isFormValid) {
          console.log("Form is invalid:", this.errors);
          return;
        }
  
        console.log("Form is valid, calculating eligibility...");
        const principal = this.monthlyIncome * 60 - this.existingEMI;
        const rate = this.interestRate / 1200;
        const months = this.tenure * 12;
  
        if (rate === 0) {
          console.error("Interest rate cannot be zero.");
          return;
        }
  
        this.eligibilityAmount = Math.max(principal, 0); // Ensuring positive value
        this.monthlyEMI = (principal * rate) / (1 - Math.pow(1 + rate, -months));
        this.totalPayableAmount = this.monthlyEMI * months;
  
        console.log("Loan Eligibility Calculated:", this.eligibilityAmount, "EMI:", this.monthlyEMI);
      },
    },
  };
  </script>
  
  <style scoped>
  .housingheading {
    text-align: left;
    margin-bottom: 15px;
    margin-left: 20px;
  }
  
  .housing-loan-calculator {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    padding: 20px;
    min-width: 500px;
  }
  
  .calculator-container {
    width: 100%;
    max-width: 600px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* Three columns */
    grid-template-rows: repeat(2, auto); /* Two rows */
    gap: 15px; /* Adds space between fields */
  }
  
  .form-group {
    display: flex;
    flex-direction: column;
  }
  
  .result-container {
    width: 100%;
    max-width: 400px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .result {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  input,
  select {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 6px;
    border: 1px solid #ccc;
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
    margin-top: 10px;
  }
  
  button:hover {
    background: #0056b3;
  }
  
  button:disabled {
    background: #ccc;
    cursor: not-allowed;
  }
  
  .error {
    color: red;
    font-size: 14px;
  }
  </style>
   -->






   <template>
    <h1 class="housingheading">Calculate Housing Loan Eligibility</h1>
    <div class="housing-loan-calculator">
      <div class="calculator-container">
        <form @submit.prevent="calculateEligibility">
          <div class="grid-container">
            <div class="form-group">
              <label>Your Age:</label>
              <input type="number" v-model="age" @input="validateAge" required />
              <span v-if="errors.age" class="error">{{ errors.age }}</span>
            </div>
  
            <div class="form-group">
              <label>Occupation:</label>
              <select v-model="occupation">
                <option value="Salaried">Salaried</option>
                <option value="Self-Employed">Self-Employed</option>
              </select>
            </div>
  
            <div class="form-group">
              <label>Monthly Income:</label>
              <input type="number" v-model="monthlyIncome" @input="validateIncome" required />
              <span v-if="errors.monthlyIncome" class="error">{{ errors.monthlyIncome }}</span>
            </div>
  
            <div class="form-group">
              <label>Existing EMI:</label>
              <input type="number" v-model="existingEMI" @input="validateEMI" required />
              <span v-if="errors.existingEMI" class="error">{{ errors.existingEMI }}</span>
            </div>
  
            <div class="form-group">
              <label>Rate of Interest (%):</label>
              <input type="number" v-model="interestRate" step="0.1" @input="validateInterestRate" required />
              <span v-if="errors.interestRate" class="error">{{ errors.interestRate }}</span>
            </div>
  
            <div class="form-group">
              <label>Tenure (Years):</label>
              <select v-model="tenure">
                <option v-for="year in 26" :key="year" :value="year + 4">{{ year + 4 }}</option>
              </select>
            </div>
          </div>
  
          <button type="submit" :disabled="!isFormValid">Calculate Eligibility</button>
  
          <!-- Monthly EMI and Loan Eligibility Below Submit Button -->
          <div v-if="eligibilityAmount !== null" class="emi-container">
            <h3>Eligible Loan Amount: ₹{{ eligibilityAmount.toLocaleString() }}</h3>
            <h3>Monthly EMI: ₹{{ monthlyEMI.toFixed(2).toLocaleString() }}</h3>
          </div>
        </form>
      </div>
  
   
      <div v-if="eligibilityAmount !== null" class="graph-container">
        <LoanChart :loanAmount="eligibilityAmount" :totalPayableAmount="totalPayableAmount" />
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
        errors: {}, // Ensuring reactivity
      };
    },
    computed: {
      isFormValid() {
        return Object.keys(this.errors).length === 0;
      },
    },
    methods: {
      validateAge() {
        if (!this.age || this.age < 18 || this.age > 70) {
          this.errors.age = "Age must be between 18 and 70.";
        } else {
          delete this.errors.age;
        }
      },
  
      validateIncome() {
        if (!this.monthlyIncome || this.monthlyIncome < 30000) {
          this.errors.monthlyIncome = "Income must be at least ₹30,000.";
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
        console.log("Button clicked, checking form validity...");
        if (!this.isFormValid) {
          console.log("Form is invalid:", this.errors);
          return;
        }
  
        console.log("Form is valid, calculating eligibility...");
        const principal = this.monthlyIncome * 60 - this.existingEMI;
        const rate = this.interestRate / 1200;
        const months = this.tenure * 12;
  
        if (rate === 0) {
          console.error("Interest rate cannot be zero.");
          return;
        }
  
        this.eligibilityAmount = Math.max(principal, 0); // Ensuring positive value
        this.monthlyEMI = (principal * rate) / (1 - Math.pow(1 + rate, -months));
        this.totalPayableAmount = this.monthlyEMI * months;
  
        console.log("Loan Eligibility Calculated:", this.eligibilityAmount, "EMI:", this.monthlyEMI);
      },
    },
  };
  </script>
  
  <style scoped>
  .housingheading {
    text-align: left;
    margin-bottom: 15px;
    margin-left: 24px;
  }
  
  .housing-loan-calculator {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    padding: 20px;
    min-width: 600px;
  }
  
  .calculator-container {
    width: 100%;
    max-width: 677px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, auto);
    gap: 15px; 
  }
  
  .form-group {
    display: flex;
    flex-direction: column;
  }
  
  .emi-container {
    margin-top: 15px;
    font-size: 18px;
    font-weight: bold;
    
    text-align: center;
    background: #f9f9f9;
    padding: 10px;
    border-radius: 8px;
    border: none;
    box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .graph-container {
    width: 100%;
    max-width: 400px;
    padding: 20px;
    border-radius: 12px;
    background: white;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  input,
  select {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 6px;
    border: 1px solid #ccc;
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
    margin-top: 10px;
  }
  
  button:hover {
    background: #0056b3;
  }
  
  button:disabled {
    background: #ccc;
    cursor: not-allowed;
  }
  
  .error {
    color: red;
    font-size: 14px;
  }
  </style>
  