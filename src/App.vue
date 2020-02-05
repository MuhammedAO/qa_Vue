/* eslint-disable no-console */
/* eslint-disable no-console */
<template>
  <div id="app">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length > 0"
            :currentQuestion="questions[index]"
            :next="next"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox
  },

  data() {
    return {
      questions: [],
      index: 0
    };
  },
  methods: {
    next() {
      this.index++;
    }
  },
  mounted: async function() {
    let res = await fetch(
      "https://opentdb.com/api.php?amount=10&type=multiple",
      {
        method: "get"
      }
    );

    let json = await res.json();

    this.questions = json.results;

    // eslint-disable-next-line no-console

    // eslint-disable-next-line no-console
    // .then(res => (res.json()))

    // .then((jsonData) => {
    //  this.questions = jsonData.results
    // })
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
