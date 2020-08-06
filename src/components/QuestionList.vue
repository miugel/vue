<template>
  <div class="container">
    <h1>Quiz 1 - HTML/CSS/JS Practice</h1>
  </div>
</template>

<script>
  import questions from '../questions.json';

  export default {
    name: 'QuestionList',
    questions: questions
  }
</script>

<style scoped>
  .container {
    margin: 0 auto;
    width: 90%;
  }

  h1 {
    color: #2c3e50;
    font-size: 24px;
    margin: 16px 0;
  }

  @media (min-width: 1024px) {
    .container {
      width: 921.6px;
    }
  }
</style>
