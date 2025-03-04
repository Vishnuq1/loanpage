

   <template>
    <div class="faq-container">
      <h1 class="faqheading">
  <span class="bold-faq">Frequently Asked Questions</span><br>About Home Loans
</h1>

  
      <!-- Buttons to switch FAQ sets -->
      <div class="faq-button-group">
        <button class="faq-button" :class="{ active: activeSet === 1 }" @click="showQuestions(1)">HOME</button>
        <button class="faq-button" :class="{ active: activeSet === 2 }" @click="showQuestions(2)">BANKS</button>
        <button class="faq-button" :class="{ active: activeSet === 3 }" @click="showQuestions(3)">LOAN EMI</button>
        <button class="faq-button" :class="{ active: activeSet === 4 }" @click="showQuestions(4)">LOAN ELIGIBILITY</button>
      </div>
  
      <!-- Questions and Answers -->
      <div class="faq-question-box">
        <ul>
          <li v-for="(item, index) in questions" :key="index">
            <div class="faq-question" @click="toggleAnswer(index)">
              {{ item.question }}
              <span class="faq-arrow">{{ activeIndex === index ? "▲" : "▼" }}</span>
            </div>
            <transition name="fade">
              <p v-if="activeIndex === index" class="faq-answer">{{ item.answer }}</p>
            </transition>
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from "vue";
  
  export default {
    setup() {
      const questions = ref([]);
      const activeIndex = ref(null);
      const activeSet = ref(1);
  
      const faqSet1 = [
        { question: "What is Vue.js?", answer: "Vue.js is a progressive JavaScript framework for building UIs." },
        { question: "How does Vue.js work?", answer: "Vue uses a virtual DOM and reactive components." },
        { question: "What are Vue components?", answer: "Components are reusable pieces of UI in Vue." },
      ];
  
      const faqSet2 = [
        { question: "How to install Vue.js?", answer: "You can install Vue.js using npm: `npm install vue`." },
        { question: "What’s new in Vue 3?", answer: "Vue 3 introduces Composition API and better reactivity." },
        { question: "What is Vue Router?", answer: "Vue Router is the official routing library for Vue.js." },
      ];
  
      const faqSet3 = [
        { question: "How does Vue reactivity work?", answer: "Vue tracks dependencies and updates automatically." },
        { question: "What is Vuex?", answer: "Vuex is a state management library for Vue applications." },
        { question: "How to use Vue directives?", answer: "Directives like v-if and v-for control the DOM dynamically." },
      ];
  
      const faqSet4 = [
        { question: "What is the Vue Composition API?", answer: "It allows better organization of logic in Vue 3." },
        { question: "How to handle events in Vue?", answer: "Use `v-on` or `@click` to handle events." },
        { question: "What are Vue lifecycle hooks?", answer: "They let you run code at different stages of a component's life." },
      ];
  
      onMounted(() => {
        showQuestions(1);
      });
  
      const showQuestions = (set) => {
        questions.value = set === 1 ? faqSet1 :
                          set === 2 ? faqSet2 :
                          set === 3 ? faqSet3 : faqSet4;
        activeSet.value = set;
        activeIndex.value = null;
      };
  
      const toggleAnswer = (index) => {
        activeIndex.value = activeIndex.value === index ? null : index;
      };
  
      return { questions, showQuestions, toggleAnswer, activeIndex, activeSet };
    },
  };
  </script>
  
  <style scoped>
  /* Container */
  .faqheading {
  font-size: 28px; /* Adjust size as needed */
  font-weight: normal;
  text-align: left; /* Align text to the left */
  line-height: 1; /* Remove extra space between lines */
  margin-bottom: 5px; /* Remove bottom margin */
  margin-left: 0px; /* Align to the left */
}

.bold-faq {
  font-weight: 600; /* Bold text for "Frequently Asked Questions" */
}

  ul {
  list-style: none; /* Removes default bullet points */
  padding: 0; /* Removes default padding */
  margin: 0; /* Removes default margin */
}

  li {
  margin-bottom: 10px;
  border-bottom: 1px solid #ddd; /* Adds a light gray separation line */
  padding-bottom: 10px; /* Adds spacing before the line */
}

li:last-child {
  border-bottom: none; /* Removes the line after the last question */
}
.faqheading{
  text-align: left;
}

  /* Button group */
  .faq-button-group {
    display: flex;
    justify-content: left;
    gap: 10px;
    margin-bottom: 15px;
    margin-top: 30px;

  }
  
  /* FAQ Buttons */
  .faq-button {
    padding: 10px 15px;
    font-size: 16px;
  
    width:141px;
    height:50px;
    /* width:250px;
    height:60px; */
    cursor: pointer;
    border: 1px solid black;
    background-color: #fffdfd; 
    color: black;
    border-radius: 5px;
    transition: background-color 0.2s ease;
  }
  
  .faq-button.active, .faq-button:hover {
    background-color: #007bff;
    color: white;
  }
  
  /* Question Box */
  .faq-question-box {
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 8px;
    width:1104px;
    height: 559px;
    background-color: #FCF8F8 ;
 
  }
 
  /* Questions */
  .faq-question {
    font-weight: bold;
    cursor: pointer;
    padding: 10px;
    /* background-color: #eee; */
    background-color: #FCF8F8;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: background-color 0.3s;
  }
  
  .faq-question:hover {
    background-color: #ddd;
  }
  
  /* Answer */
  .faq-answer {
    padding: 10px;
    background-color: #f5f5f5;
    border-left: 3px solid #007bff;
    margin-top: 5px;
    border-radius: 5px;
  }
  
  /* Smooth dropdown effect */
  .fade-enter-active, .fade-leave-active {
    transition: max-height 0.3s ease-out, opacity 0.3s;
  }
  
  .fade-enter, .fade-leave-to {
    max-height: 0;
    opacity: 0;
    overflow: hidden;
  }
  
  .fade-enter-to, .fade-leave {
    max-height: 100px;
    opacity: 1;
  }
  
  /* Arrow icon */
  .faq-arrow {
    font-size: 14px;
    color: #555;
  }
  </style>
  