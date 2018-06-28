<template>
         <div class='game d-flex align-items-center'>

    <div class="container fluid">

        <b-card bg-variant="dark" text-variant="white">
        <question v-bind:question='question'></question>
        <answers v-bind:answers='object' v-on:nextQuestion='getQuestion($event)'>
</answers>
        </b-card>
    </div>
    </div>
</template>
<script>
import Questions from "./Questions.vue";
import Answers from "./Answers.vue";

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
    answers: Answers
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
