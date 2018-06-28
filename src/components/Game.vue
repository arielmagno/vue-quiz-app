<template>
<div class="container fluid">
    <div class="card">
        <b-card bg-variant="dark" text-variant="white">
        <h1 class="text-center"><question v-bind:question='question'></question></h1>
        <h3><answers v-bind:answers='object' v-on:nextQuestion='getQuestion($event)'>
</answers></h3>
        <h3><span> Score</span> <p>{{this.result.corrects}}</p></h3>
        </b-card>
    </div>
</div>
</template>
<script>
import Questions from "./Questions.vue";
import Answers from "./Answers.vue";
import Score from "./Score.vue"

export default {
  data: function() {
    return {
      questions: this.$store.state.questions,
      question: "",
      //carry the active question on page
      object: {},
      result: {
        corrects: 0,
        incorrects: 0
      },
      gameActive: true
    };
  },
  components: {
    question: Questions,
    answers: Answers,
    score: Score
  },
  methods: {
    getQuestion: function(answer) {
      // update score
      console.log("Score" + this.result.corrects);
      if (answer) {
        this.result.corrects++;
      } else if (answer == false) {
        this.result.incorrects;
      } else if (answer == null) {
      }
      if (this.questions[0]) {
        this.gameActive = true;
        this.object = this.questions.shift();
        this.question = this.object.question;
      } else {
        this.$store.commit("setResults", this.result);
        this.$router.push({ name: "results" });
      }
    }
  },
  created() {
    this.getQuestion();
    console.log("Created" + this.questions);
  }
};
</script>
<style scoped>
p{
  font-size:20px; 
}
</style>
