<template>
  <div>
    <h1 v-html="this.question"></h1>
    <input type="radio" value="" />
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      question: undefined,
      incorrectAnswers: [],
      correctAnswer: undefined,
    };
  },
  computed: {
    answers() {
      var answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      answers.push(this.correctAnswer);
      console.log(answers);
      return answers;
    },
  },
  created() {
    axios
      .get(
        "https://opentdb.com/api.php?amount=10&category=18&difficulty=easy&type=boolean"
      )
      .then((response) => {
        this.question = response.data.results[0].question;
        this.incorrectAnswers = response.data.results[0].incorrect_answers;
        this.correctAnswer = response.data.results[0].correct_answer;
        console.log(response.data.results);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px auto;
  max-width: 960px;
}
</style>
