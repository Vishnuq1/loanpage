<script>
import axios from "axios";

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
  <div class="credit-score-container">
 

    <div class="form-box">
        <h2>Enter your details to access your
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
  </div>
</template>

<style>
.credit-score-container {
  text-align: center;
  margin-top: 20px;
}

/* Form Box with Outline */
.form-box {
  border: 2px solid #007bff;
  padding: 20px;
  border-radius: 10px;
  width: 350px;
  margin: 20px auto;
  background: #f8f9fa;
}

/* Input Styles */
.input-group {
  position: relative;
  width: 100%;
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
  background-color: #007bff;
  margin-top: -3px;
}

/* Checkbox Group */
.checkbox-group {
  display: flex;
  /* align-items: right; */
  justify-content: flex-start; 
  gap: 8px;
  margin-top: 10px;
  font-family: 'Roboto', sans-serif;
  font-weight: 200;
  size: 15px;
  line-height: 17.58px;
  opacity: 0.6;
 
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
  margin: 10px;
  padding: 8px 15px;
  cursor: pointer;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  width: 100%;
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
