<template>
   <div class="one">
    <div class="partner_banks">
    <div>
      <h1>Partners Bank</h1>
      
    </div>

<div class="sbi">


  <div class="sbi-container">
    <!-- SBI Logo on the left -->
    <img :src="sbiLogo" alt="SBI Logo" class="sbi-logo" />

    <!-- Bank Name on the right -->
    <h2 class="sbi-title">State Bank Of India</h2>
  </div>


<div class="detail"> 
<div class="a">
<h4>Loan Type</h4>
<h5>Home Loan</h5>
</div>

<div class="a">
    <h4>Interest Rate</h4>
    <h5>Starting From</h5>
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


  <div class="sbi-container">
    <!-- SBI Logo on the left -->
    <img :src="pnbLogo" alt="SBI Logo" class="sbi-logo" />

    <!-- Bank Name on the right -->
    <h2 class="sbi-title">Punjab National Bank</h2>
  </div>



<div class="detail">
    <div class="a">
<h4>Loan Type</h4>
<h5>Home Loan</h5>
</div>

<div class="a">
    <h4>Interest Rate</h4>
    <h5>Starting From</h5>
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
  <div class="sbi-container">
    <!-- SBI Logo on the left -->
    <img :src="axisLogo" alt="SBI Logo" class="sbi-logo" />

    <!-- Bank Name on the right -->
    <h2 class="sbi-title">    Axis Bank</h2>
  </div>


<div class="detail">
    <div class="a">
        <h4>Loan Type</h4>
        <h5>Home Loan</h5>
</div>

<div  class="a">
    <h4>Interest Rate</h4>
    <h5>Starting From</h5>
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
  <div class="sbi-container">
    <!-- SBI Logo on the left -->
    <img :src="kotakLogo" alt="SBI Logo" class="sbi-logo" />

    <!-- Bank Name on the right -->
    <h2 class="sbi-title">Kotak Mahindra Bank</h2>
  </div>

<div class="detail">
    <div  class="a">
        <h4>Loan Type</h4>
        <h5>Home Loan</h5>
</div>

<div  class="a">
    <h4>Interest Rate</h4>
    <h5>Starting From</h5>
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
  <div class="sbi-container">
    <!-- SBI Logo on the left -->
    <img :src="hdfcLogo" alt="SBI Logo" class="sbi-logo" />

    <!-- Bank Name on the right -->
    <h2 class="sbi-title">HDFC Bank</h2>
  </div>

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


<input type="text" placeholder="Enter city">
<input type="text" placeholder="Enter locality">
<input type="text" placeholder="Enter pincode">
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
import sbiLogo from "@/assets/sbi.jpg"; // ✅ Import image from assets folder
import pnbLogo from "@/assets/pnb.jpg";
import axisLogo from "@/assets/axis.jpg";
import kotakLogo from "@/assets/kotak.jpg";
import bobLogo from "@/assets/bob.jpg";
import hdfcLogo from "@/assets/hdfc.jpg";

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
      professionTypes: ["Salaried", "Business", "  Self Employed "],
      sbiLogo, // ✅ Assign imported image to a variable
      pnbLogo,
      axisLogo,
      kotakLogo,
      bobLogo,
      hdfcLogo,

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
  gap: 140px; 
  position: relative; 
}

.enquiry_form {

  /* padding: 20px;
  text-align: left;
  overflow: visible;
  border: 1px solid #cdcdcd;
  border-radius: 10px; 
  max-width: 500px;
  height: 112vh; */

  padding: 20px;
  text-align: left;
  border: 1px solid #cdcdcd;
  border-radius: 10px;
  max-width: 500px;
  height: auto; /* Adjust height dynamically */
  position: sticky;
  top: 20px; /* Stick to top when scrolling */
  align-self: flex-start; /* Aligns to the top of flex container */
}
.partner_banks {
flex: 1;



  padding: 20px 20px 5px 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 10px;
  /* max-width: 500px */
  min-width: 500px;
}
.headinglogo{
  display:flex;
  justify-items: left;
  justify-content: left;
  margin-left: 0;
  padding-left: 0;
  padding-right: 20px;
}
.sbi{
    outline: 1px solid rgb(10, 10, 10);
    outline-offset: 5px; 
  
  margin: 40px; 

  text-align: center;
  background: white;

  padding: 5px 5px 10px 5px;
  border-radius: 8px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1); 
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  gap: 10px; /* ✅ Spacing between logo and text */

}

.sbi-container {
  display: flex;
  align-items: left;
  gap: 10px; /* Space between logo & text */
 padding-left: 0;
}
.sbi-title {
  margin: 0;
  font-size: 22px;
  padding-top: 15px;
}
.sbi:hover {
  transform: translateY(-5px); 
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3); 
}
.sbi-logo {
  width: 100px; /* ✅ Resize image */
  height: auto;
  margin-left: 0;
}

.detail{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    padding-top: 5px;
    padding-top: 5px;
}
.a h4, 
.a h5 {
  margin: 0; 
  padding: 2px; 
  line-height: 1;
}
.enq{
    text-align: center;
}
.placeholder_detail1 p {
  margin-top: 5px;
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
  
  margin-top: 5px;
  margin-bottom: 5px; 
  gap: 50px; /* Adds space between input fields */
}

.address input {
  width: 75%; /* Adjust width as needed */
  text-align: center;
  height: 30px;
  font-size: 15px;
  /* padding: 10px; */
  border: 2px solid #ccc;
  border-radius: 5px;
  margin-top: 5px;
  margin-bottom: 5px; 
}
.btn_loan {
  display: flex;
  justify-content: center; /* Center buttons */
  gap: 20px; /* Space between buttons */
  margin-top: 5px;
  margin-bottom: 15px; 
 
  
 
}









.btn_loan button {
    text-align: center;
  padding: 0px 30px; /* Bigger padding for larger size */
  font-size: 15px; /* Increase font size */
  font-weight: lighter; /* Make text bold */
  width: 250px; /* Set a fixed width */
  height: 60px; /* Set a fixed height */
  border: 1px solid black;
  background-color: #ffffff; 
  color: rgb(7, 7, 7);
  border-radius: 10px; /* Rounded edges */
  cursor: pointer;
  transition: transform 0.2s, background-color 0.3s;

}

.btn_loan button:hover {
  background-color: #6FA1FF; /* Darker blue on hover */
  transform: scale(1.05); /* Slight zoom effect */
  color: white;
  font-weight: bold;
}

.profession {
  padding-top: 5px;
  display: flex;
  gap: 15px; /* Space between buttons */
  flex-wrap: nowrap; /* Prevents wrapping to the next line */
  justify-content: center; /* Centers buttons */
}

.profession button {
  text-align: center;
  padding: 10px 30px; /* Bigger padding for larger size */
  font-size: 16px; /* Increase font size */
  font-weight: lighter; /* Make text bold */
  width: 250px; /* Set a fixed width */
  height: 60px; /* Set a fixed height */
  border: 1px solid black;
  background-color: #ffffff; /* Match Loan Type button color */
  color: #000000; /* White text */
  border-radius: 10px; /* Rounded edges */
  cursor: pointer;
  transition: transform 0.2s, background-color 0.3s;
}


.profession button:hover {
  background-color: #6FA1FF; /* Same hover effect as loan type */
  transform: scale(1.05); /* Slight zoom effect */
  color: white;
  font-weight: bold;
}

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

/* button {
  padding: 10px 20px;
  border: 2px solid #ccc;
  background-color: #fbfbfb;
  cursor: pointer;
  transition: 0.3s;
} */
button {
    margin: 10px;
    padding: 8px 15px;
    cursor: pointer;
    border: none;
    background-color: #6FA1FF;
    color: white;
    border-radius: 5px;
    width: 100%;
}
button:hover {
  background-color: #6FA1FF;
}

/* Highlight selected button in blue */
button.selected {
  background-color: #6FA1FF;
  color: white;
  /* border-color: blue; */
}


</style>

