<template>
   <div class="faq-container">
    <h2>Frequently asked question about Home Loans</h2>
    <!-- Buttons to switch FAQ sets -->
    <div class="button-group">
      <button :class="{ active: activeSet === 1 }" @click="showQuestions(1)">HOME</button>
      <button :class="{ active: activeSet === 2 }" @click="showQuestions(2)">BANKS</button>
      <button :class="{ active: activeSet === 3 }" @click="showQuestions(3)">LOAN EMI</button>
      <button :class="{ active: activeSet === 4 }" @click="showQuestions(4)">LOAN ELIGIBILITY</button>
    </div>

    <!-- Questions and Answers -->
    <div class="question-box">
      
      <ul>
        <li v-for="(item, index) in questions" :key="index">
          <div class="question" @click="toggleAnswer(index)">
            {{ item.question }}
            <span class="arrow">{{ activeIndex === index ? "▲" : "▼" }}</span>
          </div>
          <transition name="fade">
            <p v-if="activeIndex === index" class="answer">{{ item.answer }}</p>
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

    // Show FAQ Set 1 by default
    onMounted(() => {
      showQuestions(1);
    });

    const showQuestions = (set) => {
      if (set === 1) questions.value = faqSet1;
      else if (set === 2) questions.value = faqSet2;
      else if (set === 3) questions.value = faqSet3;
      else if (set === 4) questions.value = faqSet4;

      activeSet.value = set;
      activeIndex.value = null; // Reset active answer when switching sets
    };

    const toggleAnswer = (index) => {
      activeIndex.value = activeIndex.value === index ? null : index;
    };

    return { questions, showQuestions, toggleAnswer, activeIndex, activeSet };
  },
};
  </script>
  
  <style>
  .faq-container {
    text-align: center;
    margin: 20px;
  }
  
  .button-group {
    display: flex;
    justify-content: center;
    margin-bottom: 15px;
  }
  
  button {
    margin: 10px;
    padding: 10px 15px;
    font-size: 16px;
    cursor: pointer;
    border: none;
    background-color: #ccc;
    color: black;
    border-radius: 5px;
    transition: 0.3s;
  }
  
  button.active {
    background-color: #007bff;
    color: white;
  }
  
  button:hover {
    background-color: #0056b3;
    color: white;
  }
  
  .question-box {
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #efe4ef99;
  }
  
  ul {
    list-style: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 10px;
  }
  
  .question {
    font-weight: bold;
    cursor: pointer;
    padding: 10px;
    background-color: #eee;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: background 0.3s;
  }
  
  .question:hover {
    background-color: #ddd;
  }
  
  .answer {
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
  
  .arrow {
    font-size: 14px;
    color: #555;
  }
  </style>
  