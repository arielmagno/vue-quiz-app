<template>
<div class="container fluid" style="width:100%; height:800px" >
    <div class="card text-center" id="card-container">
        <b-card bg-variant="dark" text-variant="white" style="width:100%; height:780px">
          <br><br>
        <h1 class="text-center"><question v-bind:question='question'></question></h1>
        <br>
        <br><br>

        <h3 class="text-center"><answers  v-bind:answers='object' v-on:nextQuestion='getQuestion($event)'>
</answers></h3>
<br><br>
        <h1 class="text-center"><span> Score: {{this.result.corrects}}</span>
        </h1>
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

#card-container{
  border: groove 15px
}



.center{
  align-content: flex;
}


</style>
