<script>
import FAQ from '@/components/FAQ.vue';
import LoanDetails from './components/LoanDetails.vue';
import EmiDetail from './components/EmiDetail.vue';
import EmiChart from './components/EmiChart.vue';
import CreditScore from './components/CreditScore.vue';
import HousingLoan from './components/HousingLoan.vue';
import LoanChart from './components/LoanChart.vue';
// import CreditScoreChart from './components/CreditScoreChart.vue';



export default {
  name: 'App',
  components: {
    LoanDetails,
    HousingLoan,
    // LoanChart,
    EmiDetail,
    // EmiChart,
   
    CreditScore,
    // CreditScoreChart,
  
    FAQ
  }
};
</script>

<template>
  <div id="app">
    <!-- <header>
      <h1>Welcome to the FAQ Page</h1>
    </header> -->
    <main>
      <LoanDetails/>
      <br>
      <br>
  
      <!-- <LoanChart/> -->
      <br>
       <EmiDetail/>
       <br>
       <br>
       <!-- <EmiChart/> -->
       <br>
       <HousingLoan/>
       <br>
       <CreditScore/>
       <!-- <CreditScoreChart/> -->
       <br>
       <br>
      <FAQ />
    </main>
  </div>
</template>

<style scoped>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  margin-top: 20px;
  
}
header {
  background: #f8f9fa;
  padding: 20px;
  border-bottom: 2px solid #ddd;
}
</style>
