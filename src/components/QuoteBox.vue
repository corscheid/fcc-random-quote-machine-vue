<template>
  <div id="quote-box">
  <h1 id="text"><i class="fa fa-quote-left"></i> {{ quote }}</h1>
  <p id="author">- {{ author }}</p>
  <div class="btn-row">
    <button class="btn btn-primary" id="new-quote" @click="getNewQuote()">
      New quote
    </button>
    <a
      id="tweet-quote"
      :href="tweetURL"
      target="_top"
      class="btn btn-secondary"
    >
      <i class="fa fa-twitter"></i> Tweet
    </a>
  </div>
</div>
</template>

<script>
export default {
  name: "QuoteBox",
  props: {
    quote: String,
    author: String,
    tweetURL: String,
    getNewQuote: Function
  }
}
</script>

<style lang="scss" scoped>
$white: #fafafa;
$black: #3f3f3f;

#quote-box {
  padding: 2em;
  background-color: $white;
  margin: 20%;
  border-radius: 10px;
  color: $black;

  #text {
    font-family: 'Amiri', serif;
  }
  #author {
    font-family: 'Neucha', cursive;
    font-size: 2.5em;
  }
  .btn-row {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;

    #tweet-quote {
      margin-left: 1em;
    }
  }
}

@media only screen and (max-width: 480px) {
  #quote-box {
    margin: 0;
    overflow-y: auto;
  }
}
</style>