<template>
  <div class="container">
    <div class="inner-container">
      <p>Quiz Application</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Header'
  };
</script>

<style scoped>
  .container {
    background-color: maroon;
    color: white;
    display: flex;
    align-items: center;
    height: 48px;
  }
  
  .inner-container {
    margin: 0 auto;
    width: 90%;
  }
</style>
