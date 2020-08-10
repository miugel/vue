<template>
  <div class="question-list-container">
    <h1>{{ questions.title }}</h1>
    <Results v-if="successfullySubmitted" :questions="questions" :currentSelections="currentSelections" />
    <QuestionCard
      v-for="(question, index) in questions.questions"
      :key="index"
      :question="question"
      :questionIndex="index"
      :currentSelections="currentSelections"
      :setCurrentSelections="setCurrentSelections"
      :error="error"
      :successfullySubmitted="successfullySubmitted"
    >
    </QuestionCard>
    <button class="submit" @click="onSubmit()" :disabled="successfullySubmitted">Submit</button>
    <p class="error" v-if="error">{{ error }}</p>
  </div>
</template>

<script>
  import QuestionCard from "./QuestionCard";
  import Results from "./Results";
  import questions from "../questions.json";

  export default {
    name: "QuestionList",
    components: {
      QuestionCard,
      Results
    },
    data: () => ({
      questions: questions,
      // Array to keep track of all currently selected choices, index is the question index, choices default to undefined
      // Preallocate an array the length of the number of questions in the json file and fill it with null values
      currentSelections: Array(questions.questions.length).fill(null),
      error: null,
      successfullySubmitted: false
    }),
    methods: {
      // This will modify the current selection, keeping track of the question inputs, takes in the question's index and the choice's index as the value
      setCurrentSelections: function(questionIndex, choiceIndex) {
        this.currentSelections[questionIndex] = choiceIndex
      },
      onSubmit: function() {
        // Validate all questions are answered, if not display error message and give unanswered questions a yellow border
        const unansweredQuestions = this.currentSelections.filter(selection => selection === null);

        if (unansweredQuestions.length > 0) {
          this.error = "Answer all questions before submitting. Unanswered questions are displayed in yellow.";
        } else {
          this.error = null;
          this.successfullySubmitted = true;
          window.scrollTo({ top: 0, behavior: "smooth" });
        }
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
    display: block;
    font-size: 14px;
    font-weight: 600;
    margin: 0 auto;
    margin-bottom: 16px;
    padding: 10px 16px;
    transition: 0.5s;
  }

  .submit:hover {
    box-shadow: none;
  }

  .submit:disabled {
    opacity: 0.5;
    cursor: auto;
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
