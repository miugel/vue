<template>
  <div class="question-list-container">
    <h1>{{ questions.title }}</h1>
    <QuestionCard
      v-for="(question, index) in questions.questions"
      :key="index" :question="question"
      :questionIndex="index"
      :currentSelections="currentSelections"
      :setCurrentSelections="setCurrentSelections"
    >
    </QuestionCard>
    <button class="submit">Submit</button>
    <!-- <p class="error" v-if="error">{{ error }}</p> -->
  </div>
</template>

<script>
  import QuestionCard from "./QuestionCard";
  import questions from "../questions.json";

  export default {
    name: "QuestionList",
    components: {
      QuestionCard
    },
    data: () => ({
      questions: questions,
      currentSelections: new Array(questions.questions.length),
      error: "Answer all questions before submitting. Unanswered questions are displayed in yellow."
    }),
    methods: {
      // This will modify the current selection, keeping track of the question inputs, takes in the question's index and the choice index as the value
      setCurrentSelections: (questionIndex, value) => {
        console.log("setCurrentSelections run");
        return this.currentSelections[questionIndex] = value;
      }
    }
  };
</script>

<style scoped>
  .question-list-container {
    margin: 0 auto;
    margin-bottom: 128px;
    width: 90%;
  }

  h1 {
    color: #2c3e50;
    font-size: 24px;
    margin: 16px 0;
  }

  .submit {
    background-color: #08a05c;
    border: none;
    border-radius: 3px;
    box-shadow: 0px 3px 3px 0px #ccc;
    cursor: pointer;
    color: white;
    font-size: 14px;
    font-weight: 600;
    margin: 0 auto;
    margin-bottom: 16px;
    padding: 10px 16px;
    transition: 0.5s;

    display: block;
  }

  .submit:hover {
    box-shadow: none;
  }

  .error {
    color: #dd4b39;
    font-size: 14px;
    font-weight: 600;
    text-align: center;
  }

  @media (min-width: 1024px) {
    .question-list-container {
      width: 921.6px;
    }
  }
</style>
