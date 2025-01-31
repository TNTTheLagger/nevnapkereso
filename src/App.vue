<template>
  <div id="app" class="container py-4">
    <!-- Title centered above everything -->
    <h1 class="text-center mb-4">Névnap Kereső</h1>

    <!-- Search Form and Results Container -->
    <div class="row">
      <!-- Search Form Component -->
      <div class="col-md-6">
        <div class="border p-4 rounded shadow-sm">
          <SearchForm @search="search" />
        </div>
      </div>

      <!-- Results Display Component -->
      <div class="col-md-6">
        <div class="border p-4 rounded shadow-sm">
          <ResultsDisplay :result="result" :error="error" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchForm from "./components/SearchForm.vue";
import ResultsDisplay from "./components/ResultsDisplay.vue";

export default {
  name: "App",
  components: {
    SearchForm,
    ResultsDisplay,
  },
  data() {
    return {
      result: null,  // API result
      error: null,   // Error message if any
    };
  },
  methods: {
    search({ date, name }) {
      this.error = null;
      this.result = null;

      let url = "/apiminta/nevnapok/";

      if (date) {
        url += `?nap=${date}`;
      } else if (name) {
        url += `?nev=${name}`;
      } else {
        this.error = "Kérjük, adjon meg egy dátumot vagy egy nevet!";
        return;
      }

      fetch(url)
        .then(response => {
          if (!response.ok) {
            throw new Error("Hiba történt a keresés során!");
          }
          return response.json();
        })
        .then(data => {
          if (data.hiba) {
            this.error = data.hiba;
          } else {
            this.result = data;
          }
        })
        .catch(() => {
          this.error = "Hiba történt a keresés során!";
        });
    },
  },
};
</script>

<style scoped>
/* All custom styles are removed, Bootstrap will handle the design */
</style>
