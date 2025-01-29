<template>
  <div class="search-form">
    <div class="mb-3">
      <label for="date" class="form-label">Keresés dátum alapján (pl. 4-30):</label>
      <input v-model="date" id="date" type="text" class="form-control" placeholder="Hónap-Nap" />
    </div>

    <div class="mb-3">
      <label for="name" class="form-label">Vagy keresés név alapján (pl. Katalin):</label>
      <input v-model="name" id="name" type="text" class="form-control" placeholder="Név" />
    </div>

    <button @click="onSearch" class="btn btn-success w-100">Keresés</button>
  </div>
</template>

<script>
export default {
  name: "SearchForm",
  data() {
    return {
      date: "",
      name: "",
    };
  },
  methods: {
    onSearch() {
      // Emit event to parent (App.vue) with search parameters
      this.$emit("search", { date: this.date, name: this.name });
    },
  },
};
</script>

<style scoped>
/* All custom styles are removed, Bootstrap will handle the design */
</style>
