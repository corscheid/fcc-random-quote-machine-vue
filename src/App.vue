<template>
  <div id="app">
    <div v-if="loading">
      <h1>loading...</h1>
    </div>
    <QuoteBox v-else
      :quote="quote.quote"
      :author="quote.author"
      :tweetURL="tweetURL"
      :getNewQuote="getNewQuote"
    ></QuoteBox>
  </div>
</template>

<script>
import QuoteBox from "./components/QuoteBox.vue";

export default {
  name: "App",
  components: {
    QuoteBox
  },
  data() {
    return {
      loading: true,
      quote: {},
      quoteList: [],
      tweetURL: ""
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      const quotesURL = "https://gist.githubusercontent.com/camperbot/5a022b72e96c4c9585c32bf6a75f62d9/raw/e3c6895ce42069f0ee7e991229064f167fe8ccdc/quotes.json";
      const response = await fetch(quotesURL);
      const quotes = await response.json();
      const idx = Math.floor(Math.random() * quotes.quotes.length);
      const newQuote = quotes.quotes[idx];
      this.quoteList = quotes.quotes;
      this.quote = newQuote;
      this.tweetURL = `https://twitter.com/intent/tweet?hashtags=quotes&related=freecodecamp&text=${newQuote.quote} --${newQuote.author}`;
      this.loading = false;
    },
    getNewQuote() {
      const idx = Math.floor(Math.random() * this.quoteList.length);
      const newQuote = this.quoteList[idx];
      this.quote = newQuote;
    }
  }

}
</script>

<style lang="scss">
$white: #fafafa;

#loading {
  color: $white;
  font-family: 'Amiri', serif;
}
</style>
