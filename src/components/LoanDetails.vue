<template>
   <div class="one">
    <div class="partner_banks">
    <div>
      <h1>Partners Bank</h1>
      
    </div>

<div class="sbi">
<!-- logo of sbi will there just beside name of SBI -->
<h2>State Bank Of India</h2>

<div class="detail"> 
<div class="a">
<h4>Loan Type</h4>
<h5>Home Loan</h5>
</div>

<div class="a">
    <h4>Interest Rate</h4>
    <h5>starting From</h5>
    <h5 class="interest">8.5%</h5>
    
</div>

<div class="a">
<h4>Tenure</h4>
<h5>Starting From</h5>
<h5>5-30 years</h5>

</div>
</div>
</div>

<div class="sbi">
    <!-- logo of sbi will there just beside name of PNB -->
<h2>Punjab National Bank Of India</h2>
<div class="detail">
    <div class="a">
<h4>Loan Type</h4>
<h5>Home Loan</h5>
</div>

<div class="a">
    <h4>Interest Rate</h4>
    <h5>starting From</h5>
    <h5 class="interest">8.5%</h5>
    
</div>

<div class="a">
    <h4>Tenure</h4>
<h5>5-30 years</h5>
<h5>Starting From</h5>
</div>
</div>
</div>



<div class="sbi">
     <!-- logo of sbi will there just beside name of Axis -->
<h2>Axis Bank Of India</h2>
<div class="detail">
    <div class="a">
        <h4>Loan Type</h4>
        <h5>Home Loan</h5>
</div>

<div  class="a">
    <h4>Interest Rate</h4>
    <h5 class="interest">8.5%</h5>
    <h5>starting From</h5>
</div>

<div  class="a">
    <h4>Tenure</h4>
    <h5>Starting From</h5>
<h5>5-30 years</h5>

</div>
</div>
</div>


<div class="sbi">
     <!-- logo of sbi will there just beside name of Kotak -->
<h2>Kotak Mahindra Bank</h2>
<div class="detail">
    <div  class="a">
        <h4>Loan Type</h4>
        <h5>Home Loan</h5>
</div>

<div  class="a">
    <h4>Interest Rate</h4>
    <h5>starting From</h5>
    <h5 class="interest">8.5%</h5>
    
</div>

<div  class="a">
    <h4>Tenure</h4>
    <h5>Starting From</h5>
<h5>5-30 years</h5>

</div>
</div>
</div>


<div class="sbi">
     <!-- logo of sbi will there just beside name of hdfc -->
<h2>HDFC Bank</h2>
<div class="detail">
    <div  class="a">
        <h4>Loan Type</h4>
        <h5>Home Loan</h5>
</div>

<div  class="a">
    <h4>Interest Rate</h4>
    <h5>starting From</h5>
    <h5 class="interest">8.5%</h5>
  
</div>

<div  class="a">
    <h4>Tenure</h4>
<h5>5-30 years</h5>
<h5>Starting From</h5>
</div>
</div>
</div>
</div>


<!-- here i will add enquiry form,then in a single div then necessary changes will be made by css -->

<div class="enquiry_form">
    <h1 class="enq">Enquiry Form</h1>
<div>
<div class="placeholder_detail1">
<p>Full Name</p>
<input type="text" value="" onfocus="this.value=''" onblur="if(this.value=='')this.value='Your Name'" class="underline-input">



<div>
<p>Mobile Number</p>
<input type="text" value="" onfocus="this.value=''" onblur="if(this.value=='')this.value='Your Number'" class="underline-input">
</div>
<div>
<p>Email</p>
<input type="text" value="" onfocus="this.value=''" onblur="if(this.value=='')this.value='Your Email'" class="underline-input">
</div>
</div>


<div class="placeholder_detail">
    <h3>Address</h3>
    <div class="address">


<input type="text" placeholder="Enter your city">
<input type="text" placeholder="Enter your locality">
<input type="text" placeholder="Enter your pincode">
</div>

</div>

</div>
<!-- <div class="Buttonenq">
<div class="loan_type">
    <h3>Loan Type</h3>

 <div class="btn_loan">
  <button @click="handleClick">Home Loan</button>
  <button @click="handleClick">Balance Transfer</button>
  <button @click="handleClick">Loan Against Property</button>
</div>

</div>

<div class="profession_type">
    <h3>Profession Type</h3>
    <div class="professsion">
    
  <button @click="handleClick">Salaried</button>
  <button @click="handleClick">Business</button>
  <button @click="handleClick">Self Employed</button>

    </div>
</div>

<div class="submit">
    <form @submit.prevent="handleSubmit">
      <button type="submit" class="submit-btn">Submit</button>
    </form>
    <h4>By continuing, I agree to India Property Dekho T&C</h4>
  </div>
</div> -->
<div class="Buttonenq">
    <!-- Loan Type Section -->
    <div class="loan_type">
      <h3>Loan Type</h3>
      <div class="btn_loan">
        <button
          v-for="loan in loanTypes"
          :key="loan"
          @click="selectLoanType(loan)"
          :class="{ selected: selectedLoanType === loan }"
        >
          {{ loan }}
        </button>
      </div>
    </div>

    <!-- Profession Type Section -->
    <div class="profession_type">
      <h3>Profession Type</h3>
      <div class="profession">
        <button
          v-for="profession in professionTypes"
          :key="profession"
          @click="selectProfessionType(profession)"
          :class="{ selected: selectedProfession === profession }"
        >
          {{ profession }}
        </button>
      </div>
    </div>

    <!-- Submit Button -->
    <div class="submit">
      <form @submit.prevent="handleSubmit">
        <button type="submit" class="submit-btn">Submit</button>
      </form>
      <h4>By continuing, I agree to India Property Dekho T&C</h4>
    </div>
  </div>




</div>
</div>









    


</template>



<script>

  //   import {
  //     Chart as ChartJS,
  //     Title,
  //     Tooltip,
  //     Legend,
  //     ArcElement,
  //     CategoryScale,
  //   } from "chart.js";
    
    
  
  //   ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale);


  //   export default {
  
    
 
    
  //     data() {
  //       return {
  //         name: ""    ,
  //          loanAmount: '',
  //         tenure: '',
  //         interestRate: '',
  //         emi: null,
  //         totalPayment: null,
    
     
  //         interestAmount: null,
    
    
    
  //       };
  //     },
    
  //     methods: {
  //       showAlert() {
  //         alert("Button Clicked!");
  //       },
       
   
    
      
  //       handleSubmit() {
  //         alert("Form submitted with name: " + this.name);
  //       },
    
  //   },
  //   handleClick(event) {
  //   alert(`You clicked: ${event.target.innerText}`);
  // },
    
     
    
      
    
  //       computed: {
  //       chartData() {
  //         return {
  //           labels: ["Principal Amount", "Interest Amount"],
  //           datasets: [
  //             {
  //               data: [this.principal, this.interest],
  //               backgroundColor: ["#4CAF50", "#FF5733"], // Green & Red Colors
  //             },
  //           ],
  //         };
  //       },
  //       chartOptions() {
  //         return {
  //           responsive: true,
  //           plugins: {
  //             legend: {
  //               position: "bottom",
  //             },
  //           },
  //         };
  //       },
  //     },
  //   }
 
    


  export default {
  data() {
    return {
      selectedLoanType: "", // Store selected Loan Type
      selectedProfession: "", // Store selected Profession Type
      loanTypes: ["Home Loan", "Balance Transfer", "Loan Against Property"],
      professionTypes: ["Salaried", "Business", "Self Employed"],
    };
  },
  methods: {
    selectLoanType(loan) {
      this.selectedLoanType = loan; // Highlight selected loan type
    },
    selectProfessionType(profession) {
      this.selectedProfession = profession; // Highlight selected profession type
    },
    handleSubmit() {
      if (!this.selectedLoanType || !this.selectedProfession) {
        alert("Please select both a Loan Type and a Profession Type before submitting.");
        return;
      }
      alert(`Form submitted with Loan Type: ${this.selectedLoanType} and Profession: ${this.selectedProfession}`);
    },
  },
};
  

    </script>


<style>
.one {
  display: grid;
  grid-template-columns: 1fr 1fr; 
  gap: 60px; 
 
}

.enquiry_form {

  padding: 20px;
  text-align: left;
  overflow: visible;
  border: 1px solid #cdcdcd;
  border-radius: 10px; 
  max-width: 500px;
  height: 120vh;
}
.partner_banks {

  padding: 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 10px;
  /* max-width: 500px */
  min-width: 500px;
}
.sbi{
    outline: 1px solid rgb(10, 10, 10);
    outline-offset: 5px; 
  
  margin: 50px; 

  text-align: center;
  background: white;

  padding: 5px 10px 10px 10px;
  border-radius: 8px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1); 
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.sbi:hover {
  transform: translateY(-5px); 
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3); 
}
.detail{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
.a h4, 
.a h5 {
  margin: 0; 
  padding: 0; 
  line-height: 1;
}
.enq{
    text-align: center;
}
.placeholder_detail1 p {
  margin-bottom: 5px; /* Reduces space below labels */
}
.underline-input {
  border: none; /* Removes the box */
  border-bottom: 2px solid black; /* Adds an underline */
  outline: none; /* Removes focus outline */
  padding: 5px;
margin-bottom: 5px;
  font-size: 16px;
  width: 400px; /* Adjust width as needed */
}
.address {
  display: flex;
  gap: 50px; /* Adds space between input fields */
}

.address input {
  width: 30%; /* Adjust width as needed */
  text-align: center;
  height: 30px;
  font-size: 15px;
  /* padding: 10px; */
  border: 2px solid #ccc;
  border-radius: 5px;
}
.btn_loan {
  display: flex;
  justify-content: center; /* Center buttons */
  gap: 20px; /* Space between buttons */
 
}




.btn_loan, .profession {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 10px;
}




.btn_loan button {
    text-align: center;
  padding: 0px 30px; /* Bigger padding for larger size */
  font-size: 15px; /* Increase font size */
  font-weight: lighter; /* Make text bold */
  width: 250px; /* Set a fixed width */
  height: 50px; /* Set a fixed height */
  border: none;
  /* background-color: #007bff;  */
  /* color: rgb(7, 7, 7); */
  border-radius: 10px; /* Rounded edges */
  cursor: pointer;
  transition: transform 0.2s, background-color 0.3s;
}

.btn_loan button:hover {
  background-color: #0056b3; /* Darker blue on hover */
  transform: scale(1.05); /* Slight zoom effect */
  color: white;
  font-weight: bold;
}

.professsion {
  display: flex;
  justify-content: center; /* Center buttons */
  gap: 20px; /* Space between buttons */
  /* margin-top: 20px; */

}



/* .professsion button:hover {
    color: white;
  background-color: #0056b3; 
  transform: scale(1.05); 
} */
.submit {
  display: flex;
  flex-direction: column; /* Stack items vertically */
  justify-content: center; /* Center vertically */
  align-items: center; /* Center horizontally */
  height: 30vh; /* Full viewport height */
  text-align: center;
  margin-top: 20px; 
}

/* Style the button */

/* Hover effect */
/* .submit-btn:hover {
  background-color: #0056b3;
  transform: scale(1.1);
} */
h5 {
  opacity: 0.8; /* 0 is fully transparent, 1 is fully visible */
}
.interest{
    opacity: 1.5; 
    font-size: 16px;
}



/* try to sort extr space between submit and profession button */

.submit-btn {
  width: 280px;
  height: 70px;
  font-size: 22px;
  font-weight: bold;
  /* background-color: #007bff; */
  color: white;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-bottom: 15px; /* Space between button & text */
}
.submit form {
  margin: 0; /* Remove default margin */
}
.submit button {
  margin-top: 10px; /* Adjust spacing */
}

button {
  padding: 10px 20px;
  border: 2px solid #ccc;
  background-color: #f0f0f0;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background-color: #e0e0e0;
}

/* Highlight selected button in blue */
button.selected {
  background-color: blue;
  color: white;
  border-color: blue;
}


</style>

.professsion button {
  padding: px 40px; /* Bigger padding for larger size */
  font-size: 15px; /* Increase font size */
  font-weight: lighter; /* Make text bold */
  width: 250px; /* Set a fixed width */
  height: 50px; /* Set a fixed height */
  border: none;
  /* background-color: #007bff;  */
  color: rgb(6, 6, 6);
  border-radius: 10px; /* Rounded edges */
  cursor: pointer;
  transition: transform 0.2s, background-color 0.3s;
}

.submit-btn {
  width: 280px;
  height: 70px;
  font-size: 22px;
  font-weight: bold;
  /* background-color: #007bff; */
  color: white;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-bottom: 15px; /* Space between button & text */
}
