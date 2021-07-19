<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h3> Theme filter: </h3>
    <div>
      <button v-on:click="userFilterKey = 'movies'"> Search movies</button>
      <button v-on:click="userFilterKey= 'all'"> Search all</button>
      <button v-on:click="userFilterKey= 'games'"> Search games </button>
      <div v-for="quote in filteredQuotes" v-bind:key="quote.id">
        <p>Souce: {{ quote.source }} </p>
        <p>Quote: {{ quote.quote }} </p>
        <p>Theme: {{ quote.theme }} </p>
      </div>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      quotes: [],
      userFilterKey: "all",
    };
  },
  methods: {
    quotesIndex: function () {
      axios
        .get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json")
        .then((response) => {
          this.quotes = response.data;
        });
    },
  },
  computed: {
    filteredQuotes() {
      if (this.userFilterKey === "all") {
        return this.quotes;
      }
      return this.quotes.filter((v) => v.theme === this.userFilterKey);
    },
  },
  created: function () {
    this.quotesIndex();
  },
};
</script>