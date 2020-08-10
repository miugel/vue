<template>
  <div class="question-card-container"
    :class="{
      'unanswered-border': error && currentSelections[questionIndex] === null,
      'correct-border': successfullySubmitted && question.choices[currentSelections[questionIndex]] === question.correct_answer,
      'wrong-border': successfullySubmitted && question.choices[currentSelections[questionIndex]] !== question.correct_answer
    }"
  >
    <p class="question">{{ questionIndex + 1 }}. {{ question.question }}</p>
    <label
      v-for="(choice, choiceIndex) in question.choices"
      :key="choiceIndex"
      :class="{
        'correct-answer': successfullySubmitted
          && question.choices[currentSelections[questionIndex]] !== question.correct_answer
          && choice === question.correct_answer
      }"
    >
      <input
        :name="questionIndex + 1"
        type="radio"
        :value="choiceIndex"
        @click="setCurrentSelections(questionIndex, choiceIndex)"
        :disabled="successfullySubmitted"
      />
      {{ choice }}
    </label>
    <p class="correct" v-if="successfullySubmitted && question.choices[currentSelections[questionIndex]] === question.correct_answer">Correct</p>
    <p class="wrong" v-if="successfullySubmitted && question.choices[currentSelections[questionIndex]] !== question.correct_answer">Wrong</p>
  </div>
</template>

<script>
  export default {
    name: "QuestionCard",
    props: {
      question: Object,
      questionIndex: Number,
      currentSelections: Array,
      setCurrentSelections: Function,
      error: String,
      successfullySubmitted: Boolean
    }
  };
</script>

<style scoped>
  .question-card-container {
    background-color: white;
    border: 2px solid white;
    border-radius: 3px;
    box-shadow: 0px 3px 3px 0px #ccc;
    display: flex;
    flex-direction: column;
    margin-bottom: 16px;
    padding: 16px;
    position: relative;
    width: 100%;
  }

  .question {
    color: #2c3e50;
    font-size: 14px;
    padding-bottom: 8px;
  }

  label {
    border-radius: 3px;
    cursor: pointer;
    color: #2c3e50;
    font-size: 14px;
    padding: 8px;
    transition: 0.5s;
    width: 100%;
  }

  label:hover {
    background-color: whitesmoke;
    color: #2c3e50;
  }

  input {
    cursor: pointer;
    margin-right: 3px;
  }

  .correct {
    bottom: 4px;
    color: #08a05c;
    font-size: 14px;
    font-weight: 600;
    right: 4px;
    position: absolute;
  }

  .wrong {
    bottom: 4px;
    color: #dd4b39;
    font-size: 14px;
    font-weight: 600;
    right: 4px;
    position: absolute;
  }

  .correct-border {
    border: 2px solid #08a05c;
  }

  .wrong-border {
    border: 2px solid #dd4b39;
  }

  .unanswered-border {
    border: 2px solid #f4b400;
  }

  .correct-answer {
    background-color: #08a05c;
    color: white;
  }
</style>