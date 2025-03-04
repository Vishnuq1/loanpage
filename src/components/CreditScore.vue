<script>
import axios from "axios";
import creditpic from "@/assets/creditpic.jpg";

const imageSrc = creditpic;
export default {
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      mobileNumber: "",
      otp: "",
      requestId: "",
      isVerified: false,
      showOtpBox: false,
      agreedToIPD: false, // Controls checkbox status
      creditpic,
    };
  },
  methods: {
    async sendOTP() {
      if (!this.agreedToIPD) {
        alert("Please agree to the IPD conditions before proceeding.");
        return;
      }

      try {
        const response = await axios.post("https://third-party-otp-api.com/send", {
          mobile: this.mobileNumber,
        });

        if (response.data.success) {
          this.requestId = response.data.request_id;
          alert("OTP sent to your mobile.");
          this.showOtpBox = true;
        } else {
          alert("Failed to send OTP. Try again.");
        }
      } catch (error) {
        console.error("Error sending OTP:", error);
        alert("Error sending OTP.");
      }
    },

    async verifyOTP() {
      try {
        const response = await axios.post("https://third-party-otp-api.com/verify", {
          request_id: this.requestId,
          otp: this.otp,
        });

        if (response.data.success) {
          this.isVerified = true;
          alert("OTP Verified Successfully! Your credit score will be sent to your email.");
          this.sendCreditScoreEmail();
        } else {
          alert("Invalid OTP! Try Again.");
        }
      } catch (error) {
        console.error("Error verifying OTP:", error);
        alert("Error verifying OTP.");
      }
    },

    async sendCreditScoreEmail() {
      try {
        await axios.post("https://credit-score-api.com/send-email", {
          firstName: this.firstName,
          lastName: this.lastName,
          email: this.email,
          mobile: this.mobileNumber,
        });

        alert("Your credit score details have been emailed to you.");
      } catch (error) {
        console.error("Error sending email:", error);
        alert("Failed to send credit score email.");
      }
    }
  }
};
</script>

<template>
<h1 class="creditheading">Check Your <span class="bold-credit">Credit Score</span></h1>


  <div class="credit-score-container">
 

    <div class="form-box">
        <h2 >Enter your details to access your
            credit score</h2>
      <div class="input-group">
        <label>First Name As Per Bank record</label>
        <input type="text" v-model="firstName" required />
        <span class="underline"></span>
      </div>

      <div class="input-group">
        <label>Last Name As Per Bank record</label>
        <input type="text" v-model="lastName" required />
        <span class="underline"></span>
      </div>

      <div class="input-group">
        <label>Email As Per Bank record</label>
        <input type="email" v-model="email" required />
        <span class="underline"></span>
      </div>

      <div class="input-group">
        <label>Mobile Number As Per Bank record</label>
        <input type="tel" v-model="mobileNumber" required />
        <span class="underline"></span>
      </div>

      <!-- Checkbox for IPD Agreement -->
      <div class="checkbox-group">
        <input type="checkbox" class="box" id="ipd-agreement" v-model="agreedToIPD" />
        <label class="ipd-agr" for="ipd-agreement">By clicking the Get Free Report you hereby appoint
             India Property Dekho as your authorized representative to receive your
              credit information from Cibil and Experian. You hereby consent to such
               credit information being provided by Cibil and Experian at your registered 
               email id and also through your India Property Dekho account as per your 
               independent registration with Magicbricks subject to Terms and Conditions.</label>
      </div>

      <button @click="sendOTP" :disabled="!agreedToIPD">Send OTP</button>

      <!-- OTP Verification Box -->
      <div v-if="showOtpBox" class="otp-box">
        <h3>Enter OTP</h3>
        <div class="input-group">
          <label>OTP</label>
          <input type="text" v-model="otp" required />
          <span class="underline"></span>
        </div>
        <button @click="verifyOTP">Get Your Reports</button>
      </div>
    </div>
    <div class="creditposter">
   
      <img :src="creditpic" alt="Credit Image" />
    </div>
  </div>
</template>

<style>
.credit-score-container {
  /* text-align: center; */
  margin-top: 20px;
  display: flex;
  margin-left: 0;
  
 
}
/* .creditheading{
  text-align: left;
  margin-bottom: 45px;
  margin-left: 28px;
} */
.creditheading {
  font-size: 28px; /* Adjust as needed */
  font-weight: normal;
  text-align: left; /* Align text to the left */
  margin-bottom: 5px;
  margin-top: 15px;
}

.bold-credit {
  font-weight: 600; /* Make "Credit Score" bold */
  color: #000; /* Ensure it appears dark */
}

img {
  width: 350px;
  height: 605px;
  /* margin-top: 10px; */
  border-radius: 10px;
  margin-left: 140px;
}
/* Form Box with Outline */
.form-box {
  /* border: 1px solid #007bff;
  padding: 20px 20px 20px 20px;
  border-radius: 10px;
  width: 650px;
  margin: 0 20px 20px 0px;
  background: #ffffff;
  text-align: left; */

  /* border: 1px solid #007bff; */
  padding: 20px 20px 20px 20px;
  border-radius: 10px;
  width: 700px;
  margin: 0 20px 20px 0px;
  background: #ffffff;
  text-align: left;
  box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.2); /* Added shadow */

}

/* Input Styles */
.input-group {
  position: relative;
  width: 68%;
  margin: 15px 0;
  text-align: left;
}

label {
  font-size: 14px;
  color: #333;
  font-weight: bold;
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 5px;
  font-size: 16px;
  border: none;
  outline: none;
  background: transparent;
  text-align: left;
}

.underline {
  display: block;
  height: 2px;
  width: 100%;
  background-color: #0e0e0e;
  margin-top: -3px;
}

/* Checkbox Group */
.checkbox-group {
  display: flex;
  /* align-items: right; */
  justify-content: flex-start; 
  gap: 8px;
  margin-top: 15px;
  font-family: 'Roboto', sans-serif;
  font-weight: lighter;
  font-weight: 200;
  size: 15px;
  line-height: 17.58px;
  opacity: 0.6;
  padding-top: 10px;
  padding-bottom: 10px;
 
}

.checkbox-group input {
  width: auto;
  margin: 0;
}
.box {
  width: 19px;
  height: 20px;
  /* position: absolute;  */
  /* top: 3832px;
  left: 152px; */
  border: 1px solid black; 
}
.ipd-agr {
  width: 100%; 
  text-align: left;
}

/* Button Styles */
button {
  /* margin: 10px;
  padding: 8px 15px;
  cursor: pointer;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  width: 100%; */


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

button:disabled {
  background-color: gray;
  cursor: not-allowed;
}

/* OTP Box */
.otp-box {
  border: 2px solid #007bff;
  padding: 15px;
  margin-top: 15px;
  border-radius: 10px;
  background-color: #e6f0ff;
}
</style>
