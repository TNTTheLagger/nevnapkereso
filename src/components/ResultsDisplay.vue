<template>
    <div>
      <!-- Error Message -->
      <div v-if="error" class="alert alert-danger">
        <p>{{ error }}</p>
      </div>
    
      <!-- Result -->
      <div v-if="result">
        <div v-if="result.nevnap[0].datum" class="alert alert-info">
          <h2>Datum: {{ result.nevnap[0].datum }}</h2>
          <p v-if="result.nevnap[0].nevnap1">Névnap 1: {{ result.nevnap[0].nevnap1 }}</p>
          <p v-if="result.nevnap[0].nevnap2">Névnap 2: {{ result.nevnap[0].nevnap2 }}</p>
        </div>
      </div>
    
      <!-- No Result and No Error -->
      <div v-if="!result && !error" class="alert alert-info">
        <p>Használat: Írja be a dátumot vagy a nevet kereséshez.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "ResultsDisplay",
    props: {
      result: Object,
      error: String,
    },
  };
  </script>
  
  <style scoped>
  /* All custom styles are removed, Bootstrap will handle the design */
  </style>
  