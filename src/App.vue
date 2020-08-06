<template>
  <div id="app">
    <Header />
    <QuestionList />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import QuestionList from './components/QuestionList.vue';

export default {
  name: 'App',
  components: {
    Header,
    QuestionList
  }
};
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
  }
</style>
